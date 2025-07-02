```yaml
data_config:
  source:
    type: "disk"
    file_path: "data/code_tasks.jsonl"
    file_format: "jsonl"
  sink:
    type: "jsonl"
    file_path: "output/validated_output.jsonl"

graph_config:
  nodes:
    generate:
      node_type: llm
      output_keys: solution
      prompt:
        - system: "You are an AI that solves code problems."
        - user: "{task}"
      model:
        name: mistral
        parameters:
          temperature: 0.5
    validate:
      node_type: lambda
      lambda: validators.code.check_validity
      output_keys: 
        - is_valid
  edges:
    - from: START
      to: generate
    - from: generate
      to: validate
    - from: validate
      condition: validators.code.RouteBasedOnValidity
      path_map:
        END: END
        generate: generate

output_config:
  output_map:
    id:
      from: task_id
    solution:
      from: solution
    validity:
      from: is_valid

schema_config:
  fields:
    - name: id
      type: int
    - name: solution
      type: str
    - name: validity
      type: bool
```
