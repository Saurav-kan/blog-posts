# Reliable LLMs: Beyond the Prompt

I've recently started designing more complex RAG systems lately, learning about things like Self-RAG systems, and with that, I've been learning a lot about model output formatting. One of my favorite features that I feel so late to for not knowing about is response format.

Before I knew about this, I worked on a hackathon project called Asteria that generates a Pygame game from a user prompt. The issue was that model would try to output JSON, but half the time it would say something like "here is your JSON" before actually giving me the JSON. Or it would format it slightly differently each time. It was quite anoying to say the least. 

Thats why response formating is so usefull; Im working on a project called TracePoint which uses mutiple agent ina recursive loop, so there are a lot of small agent calls. Being able to control the exact output and output format has been super usefull to make sure the pipline doesn't constnaly break. 



```python
class ContactInfo(BaseModel):
    name: str
    email: str
schema = ContactInfo.model_json_schema()

response = client.....(
    model = ...
    reponse_format= {
        "type": "json_schema",
        "json_schema": {
            "name": "ContactInfo",
            "schema": schema
        }
    }
    ...
)
```

Pair that with Pydantic validation and the schema isn't just a hint anymore. If something's malformed, `ValidationError` tells you immediately instead of a cryptic `KeyError` three steps later.

For multi-agent systems, this is huge. Every agent in TracePoint outputs a specific structure. The model either matches it perfectly, or validation fails and I know something went wrong. No surprises downstream.

I also discovered that prompt structure matters more than tweaking temperature or top-p. Being explicit about format and giving examples does way more than parameter tuning. But structured outputs still win—they remove the guessing game entirely.

Once you have a Pydantic schema, it does double duty. Use it for the LLM response validation, then the same schema is your API contract in FastAPI. Typed inputs, validated outputs, type safety throughout. One schema doing all the work.

I'm exploring tool calling and MCP lately, which follows the same pattern—give the model less freedom, make it harder to produce garbage output. That's what reliable LLMs are really about.