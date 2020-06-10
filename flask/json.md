# Sending a JSON response

```python
from flask import json, Response

@app.route("/api/")
@app.route("/api/<idx>")
def api(idx=None):
    if not idx:
        jdata = courseData
    else:
        jdata = courseData[int(idx)]

    return Response(json.dumps(jdata), mimetype="application/json")
```

> Response cam be viewed in Inspect > Network > Response or Preview
