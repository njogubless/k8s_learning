yaml files are yaml ain't markup language
Human friendly language for data serialization standard
Used by Docker-Compose and K8S

##### Sample yaml file
```python
key:value
another_key: another value
a_umbervalue: 100

#Nesting uses identation. 2 space indent is preffered(but not required).

a_nested_map:
  key:value
  another_key" ANother Value
  another_nested_map:
    hello:hello

 # Sequences(equivalent to lists or arrays) look like this
 # (note that the (-) counts as indentation):
 a_sequence:
  - item 1
  - item 2

 # SInce yml is a susperset of JSON, you can also write JSON-sytle maps and sequences:
 json_maps: {"key":"value"}
 json_seq: [3,2,1"takeoff"]
```