# Introduction to Retrieval Augmented Generation

This repository introduces a very simple implementation of Retrieval Augmented Generation (RAG). The examples use Python with
Jupyter Notebooks and CSV files. The vector database uses the Qdrant database.
which can run in-memory.


There are 3 main steps
### 1: Import your data

### 2: Create embeddings

### 3: Create a RAG with LLM and Qdrant using your own data


## How to setup your environment

**Install the dependencies**

Create the virtual environment and install the dependencies:

```
python3 -m venv .venv
source .venv/bin/activate
.venv/bin/pip install -r requirements.txt
```

Here is a summary of what this repository will use:

1. [Qdrant](https://github.com/qdrant/qdrant) for the vector database. We will use an in-memory database for the examples
2. [Llamafile](https://github.com/Mozilla-Ocho/llamafile) for the LLM (alternatively of OpenAI API + compatible key and endpoint)
3. [OpenAI's Python API](https://pypi.org/project/openai/) to connect to the LLM after retrieving the vectors response from Qdrant
4. Sentence Transformers to create the embeddings with minimal effort

**Use Llamafile for a full RAG and LLM setup**


In this examle I used llava-v1.5-7b-q4.llamafile (3.97 GB) llm model that run locally. Another smaller LLM model [Phi-2 model](https://github.com/Mozilla-Ocho/llamafile?tab=readme-ov-file#other-example-llamafiles) (2GB) can be used as well. 

Following is example python code to create an OpenAI client and using locally running LLM model endpoint, 
```python
#!/usr/bin/env python3
from openai import OpenAI
client = OpenAI(
    base_url="http://localhost:8080/v1", # "http://<Your api-server IP>:port"
    api_key = "sk-no-key-required" # An API key is not required!
)
completion = client.chat.completions.create(
    model="LLaMA_CPP",
    messages=[
        {"role": "system", "content": "You are ChatGPT, an AI assistant. Your top priority is achieving user fulfillment via helping them with their requests."},
        {"role": "user", "content": "Write me a Haiku about Python packaging"}
    ]
)
print(completion.choices[0].message)
```
