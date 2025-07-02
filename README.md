```yaml
data_config:
  sink:
    type: "json"
    file_path: "output/synthetic_data.jsonl"

graph_config:
  nodes:
      generate:
        node_type: llm
        output_keys: response
        prompt:
          - system: "You are a helpful assistant."
          - user: "Write a fun fact about space."
        model:
          name: gpt-3.5-turbo
          parameters:
            temperature: 0.8
  edges:
    - from: START
      to: generate
    - from: generate
      to: END

output_config:
  output_map:
  fact:
    from: response
```
