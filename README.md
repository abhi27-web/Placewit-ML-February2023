```yaml
data_config:
  source:
    type: "hf"
    repo_id: "datasets-examples/doc-image-1"
    split: "train"
    streaming: true

  sink:
    type: "hf"
    repo_id: <repo_name>
    config_name: MM-doc-image-1
    split: train
    push_to_hub: true
    private: true
    token: <hf_token>

graph_config:
  nodes:
    judge_pokemon:
      output_keys: pokemon
      node_type: llm
      prompt:
        - user:
            - type: text
              text: |
                Identify the pokemon in the provided image.
            - type: image_url
              image_url: "{image}"

      model:
        name: gpt-4o
        parameters:
          max_tokens: 1000
          temperature: 0.3
  edges:
    - from: START
      to: judge_pokemon
    - from: judge_pokemon
      to: END

output_config:
    output_map:
        id:
          from: "id"
        image:
          from: "image"
        pokemon:
          from: "pokemon"
```
