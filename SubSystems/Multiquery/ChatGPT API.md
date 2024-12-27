If you want to use ChatGPT 1.0 and higher for python, you have to [follow this documentation](https://github.com/openai/openai-python)

You can also look at the default API reference, in the [Text Generation](https://platform.openai.com/docs/guides/text-generation?lang=python) section

Python syntax: 
```python
import os
from openai import OpenAI

client = OpenAI(
    api_key=os.environ.get("OPENAI_API_KEY"),  # This is the default and can be omitted
)

chat_completion = client.chat.completions.create(
    messages=[
        {
            "role": "user",
            "content": "Say this is a test",
        }
    ],
    model="gpt-4o",
)
```

Here is a [list of all parameters](https://github.com/openai/openai-python/blob/main/src/openai/types/completion_create_params.py) available to `client.create()` 


You should set `model` to `gpt-4o-mini` as it's currently the cheapest model: 
https://openai.com/api/pricing/

