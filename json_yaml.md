# JSON and YAML

### JSON
**JavaScript Object Notation** is used for transport data with attribute of key/value pairs
```json
{
  "name": "test",
  "ip": "192.168.23.45",
  "project": "DevOps",
  "website": "spartaglobal.com"

}
```
```python
import json

# read a json in a file
json = json.loads(open("example.json").read())
value = json['name']
print(value)
print(type(json))

print(json)
```
```python
import json
import os

# script to make an absolute of the json file
script_dir = os.path.dirname(__file__)
print("The script is located at: " + script_dir)
script_absolute_path = os.path.join(script_dir, 'example.json')
print("The script absolute path is: " + script_absolute_path)

# script to parse json
json = json.loads(open(script_absolute_path).read())
value = json["name"]
print(value)

# loop through json
for key in json:
    value = json[key]
    print("The key and value are {} = {}".format(key, value))
```
To parse JSON remotely, urllib module is required to allow importing json using URL 
```python
import urllib.request
import json

with urllib.request.urlopen("http://jsonplaceholder.typicode.com/todos/1") as url:
    data = json.load(url)
    print(data)
```
### YAML
**Yet Another Markup Language** is a human-readable data serialisation language and sometimes can be used instead of JSON because it is written using natural language.

#### Convert JSON to YAML
```python
import json
import os
import sys
import yaml

# How to check JSON is valid
if len(sys.argv) > 1:
    
    # open the file
    if os.path.exists(sys.argv[1]):
        source_file = open(sys.argv[1], "r")
        source_content = json.load(source_file)
        source_file.close()
    else:
        print("Error! " + sys.argv[1] + " not found")
        exit(1)

# No file, no usage
else:
    print("Usage: json_to_yaml.py <source_file.py> [target_file.yaml]")

# Processing the conversion
output = yaml.dump(source_content)

# If no target file sent to stdout
if len(sys.argv) < 3:
    print(output)

# If the target file already exists exit()
elif os.path.exists(sys.argv[2]):
    print("Error! " + sys.argv[2])

# Otherwise write to the specified file
else:
    target_file = open(sys.argv[2], "w")
    target_file.write(output)
    target_file.close()
    print("Successfully write to yaml")
```
#### Convert YAML to JSON
```python
import json
import os
import sys
import yaml

# How to check YAMl is valid
if len(sys.argv) > 1:
    # open the file
    if os.path.exists(sys.argv[1]):
        source_file = open(sys.argv[1], "r")
        source_content = yaml.safe_load(source_file)
        source_file.close()
    else:
        print("Error! " + sys.argv[1] + " not found")
        exit(1)
# No file, no usage
else:
    print("Usage: yaml_to_json.py <source_file.yaml> [target_file.json]")

# Processing the conversion
output = json.dumps(source_content, indent=2)


# If no target file sent to stdout
if len(sys.argv) < 3:
    print(output)

# If the target file already exists exit()
elif os.path.exists(sys.argv[2]):
    print("Error! " + sys.argv[2])

# Otherwise write to the specified file
else:
    target_file = open(sys.argv[2], "w")
    target_file.write(output)
    target_file.close()
    print("Successfully write to json")
```
