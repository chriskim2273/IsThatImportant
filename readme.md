# Is that Important?





## Authors

- Christopher Kim
- Antony Shen


## HuggingFace API Documentation (Source)

- https://huggingface.co/docs/api-inference/detailed_parameters
## Basic Template of How We Queried The Models

```python
import json
import requests
headers = {"Authorization": f"Bearer {API_TOKEN}"}
API_URL = "https://api-inference.huggingface.co/models/bert-base-uncased"
def query(payload):
    data = json.dumps(payload)
    response = requests.request("POST", API_URL, headers=headers, data=data)
    return json.loads(response.content.decode("utf-8"))
data = query({"inputs": "The answer to the universe is [MASK]."})
```
## List of Requirements and Libraries

- Python 3.X (and Libraries)
    - json
    - requests
    - sklearn.metrics (for precision_recall_fscore_support)
    - time
    
## Prompts

Format (with Title, Context, and Question):
```
"(title)\n(context/passage)\n(question)\n"
```

Default - Two-Shot (Two Examples) - With Title:
```
In informal games, it is customary to announce ``check'' when making a move that puts
the opponent's king in check. In formal competitions, however, check is rarely
announced.\ndo you always have to say check in chess\nFalse\nThe Jack Russell Terrier
is a small terrier that has its origins in fox hunting. It is principally white-bodied
and smooth, rough or broken-coated but can be any colour.\nis a jack russell considered
a small breed?\nTrue\n"

+

Entry from Data Set. (in same format)
    
```

One-Shot (one Example) - With Title:
```
Check (chess)\nIn informal games, it is customary to announce ``check'' when making a
move that puts the opponent's king in check. In formal competitions, however, check is
rarely announced.\ndo you always have to say check in chess\nFalse\n

+

Entry from Data Set.
```
One-Shot (no Context):
```
do you always have to say check in chess\nFalse\n

+

Entry from Data Set. (in same format)
```
For Four-Shot (if Title Required, then append to start with new line after):
```
In informal games, it is customary to announce ``check'' when making a move that 
puts the opponent's king in check. In formal competitions, however, check is rarely
announced.\ndo you always have to say check in chess\nFalse\nThe Jack Russell Terrier 
is a small terrier that has its origins in fox hunting. It is principally white-bodied
and smooth, rough or broken-coated but can be any colour.\nis a jack russell 
considered a small breed?\nTrue\nCalcium carbide is a chemical compound with the 
chemical formula of CaC. Its main use industrially is in the production of acetylene 
and calcium cyanamide.\ncalcium carbide cac2 is the raw material for the production 
of acetylene?\nTrue\nCreme eggs are available annually between 1 January and Easter 
Day. In the UK in the 1980s, Cadbury made Creme Eggs available year-round but sales
dropped and they returned to seasonal availability.\nyou can buy cadburys creme eggs
all year round?False\n"

+

Entry from Data Set. (in same format)
```
