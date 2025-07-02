```yaml
data_config:
  source:
    type: "hf"
    repo_id: "google-research-datasets/mbpp"
    config_name: "sanitized"
    split: ["train"]
    transformations:
      - transform: processors.data_transform.RenameFieldsTransform
        params:
          mapping:
            task_id: id
            overwrite: false
  sink:
    type: "jsonl"
    file_path: "output/mbpp_converted.jsonl"

graph_config:
  nodes:
    generate:
      node_type: agent
      output_keys: agent_response
      prompt:
        - system: You are an AI programming tutor.
        - user: {prompt}
      model:
        name: gpt-4
        parameters:
          temperature: 0.7
  edges:
    - from: START
      to: generate
    - from: generate
      to: END

output_config:
  generator: tasks.mbpp.code_generation_with_graph_builder.task_executor.CodeGenOutputGenerator
  output_map:
    id:
      from: id
    conversation:
      from: agent_response
      transform: build_conversation
    tags:
      value: ["mbpp", "codegen"]
    language:
      value: "en"
```
