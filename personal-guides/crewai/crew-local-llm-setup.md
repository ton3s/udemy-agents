## Local LLM Setup

1.  Install https://lmstudio.ai/

2.  In sidebar click Discover, find "hermes-3-llama-3.2-3b" (https://huggingface. co/NousResearch/Hermes-3-Llama-3.2-3B-GGUF or any other model trained to support tools), download.

3.  In sidebar click Developer, on the left - switch server to Running, on top click "Select model", find "Hermes 3 Llama 3.2 3B", click "Load model"

4.  Inside main.py (at least tested with debate crew) add only two lines, import openai, set api_base to localhost. Should look like this:

```python
# need to import to override base
import openai

def run():
    """
    Run the crew.
    """
    inputs = {
        'motion': 'There needs to be strict laws to regulate LLMs',
    }

    # set base to point to our local LM Studio
    openai.api_base = "http://localhost:1234/v1"

    try:
        result = Debate().crew().kickoff(inputs=inputs)
        print(result.raw)
    except Exception as e:
        raise Exception(f"An error occurred while running the crew: {e}")
```

Works without any problems and all locally on my (tested on Mac Air M2)

- Run the project

```
crewai run
```
