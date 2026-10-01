# AWS Cloud Engineer Journey

Week 0 starts with PropertyLite, a small Flask API that will be deployed and operated throughout the curriculum.

## Local verification

```bash
cd propertylite
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python app.py
```

In a second terminal:

```bash
curl http://localhost:8080/health
curl http://localhost:8080/properties
curl http://localhost:8080/properties/R100234
```
