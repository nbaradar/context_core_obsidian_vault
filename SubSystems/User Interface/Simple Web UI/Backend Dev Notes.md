# Plan for FastAPI Backend
#### **1. Set Up the FastAPI Application**
- Create a FastAPI app to handle API requests.
- Organize the backend into modules for scalability.
#### **2. Define API Endpoints**
- `/query`: Accept user input, run queries with your existing LLM providers, and return the results.
- `/history`: Retrieve stored queries and results from the MongoDB `result` collection.
- `/export`: Export results in Markdown or JSON format.
#### **3. Integrate Existing POC Code**
- Refactor the querying logic (`main.py`) into a service module.
- Use your MongoDB client for saving and retrieving data.
#### **4. Add Dependency Injection**
- Use FastAPI’s dependency injection to manage MongoDB connections and configurations.
---
# Pre-Dev: Install Required Dependencies
Install FastAPI, Uvicorn (server), and Motor (MongoDB driver):

```
multiquery/
|--> multiquery/
      |--> api/
            |--> __init__.py
            |--> endpoints/
                  |--> __init__.py
                  |--> query.py
                  |--> history.py
                  |--> export.py
      |--> core/
            |--> __init__.py
            |--> config.py
            |--> services/
                  |--> __init__.py
                  |--> llm_service.py
      |--> utils/
            |--> __init__.py
            |--> json_exporter.py
            |--> mongodb_client.py
      |--> app.py
|--> output/
```
## Pydantic
Python library used for **data validation and settings management**. Allows you to define schemas using Python classes and ensures that data adheres to those schemas. Often used in modern Python applications, especially with frameworks like FastAPI, because of its integration and simplicity.
### **What is Pydantic?**
Pydantic is a Python library used for **data validation and settings management**. It allows you to define schemas using Python classes and ensures that data adheres to those schemas. Pydantic is often used in modern Python applications, especially with frameworks like FastAPI, because of its integration and simplicity.
### **General Uses of Pydantic**
1. **Data Validation**:
    - Automatically validates incoming data against predefined schemas.
    - Ensures types, formats, and required fields are correct.
2. **Settings Management**:
    - Simplifies configuration loading (e.g., environment variables, config files).
    - Provides default values and validation for settings.
3. **Serialization and Deserialization**:
    - Converts data between Python objects and JSON or dictionaries seamlessly.
4. **Integration with FastAPI**:
    - Automatically generates API request and response models.
    - Provides validation for endpoint parameters and request bodies.

---
# Settings Configs using Pydantic

First set the configs using the .yaml file in `app.py`
```python
# Load configuration at startup 
	config = load_config("multiquery/config/config.yaml") 
	
def get_config(): 
	""" Dependency to provide the configuration object. """ 
	return config
```

Then import to relevant endpoint 
```python
from multiquery.app import get_config # Import get_config

@router.post("/")
async def query_api(
	prompt: str,
	config=Depends(get_config), # Inject config dependency
	collection=Depends(get_mongo_collection)
):
```

## [Dependency Injection](https://fastapi.tiangolo.com/tutorial/dependencies/) w/ FastAPI
**`get_config` Function**:
- This function acts as a **dependency provider** for the configuration object.
- It simply returns the pre-loaded `config` object from `app.py`.
**Dependency Injection in `query_api`**:
    - FastAPI’s `Depends(get_config)` automatically injects the `config` object into the `query_api` function.
**Modular Reuse**:
    - `get_config` can now be reused across all endpoints in your application without requiring repetitive imports or global variables.

So the configurations are now global and mapped to Pydantic BaseModel Configs found in `multiquery -> core -> config.py`

## Refactoring Config file
Previous config file had llms providers seperated from their configs:
```yaml
llm_providers:
  - name: chatgpt
    class_path: multiquery.llm_providers.chatgpt.ChatGPTProvider
    api_key: "YOUR_CHATGPT_API_KEY"
  - name: grok
    class_path: multiquery.llm_providers.grok.GrokProvider
    api_key: "YOUR_GROK_API_KEY"
  - name: gemini
    class_path: multiquery.llm_providers.gemini.GeminiProvider
    api_key: "YOUR_GEMINI_API_KEY"

llm_configs:
  - name: chatgpt
    model: gpt-4o-mini
    max_tokens: 100
    temperature: 0.5
```

Makes more sense to combine these:
```yaml
llms_providers:
  - name: chatgpt
	class_path: multiquery.llm_providers.chatgpt.ChatGPTProvider
	api_key: "YOUR_CHATGPT_API_KEY"
	config:
		model: gpt-4o-mini
		max_tokens: 100
		temperature: 0.5
```

And you'll need to update your Pydantic models to match the new config structure. 
Specifically, the `config.py` file which defines all mapping config objects

---
## Dependency Injection and Factory Pattern

>[!info]- **How DI and Factory Pattern Work Together**
>#### **1. DI for Configs**
>- FastAPI uses `get_config` to inject the `AppConfig` object into endpoints or services.
>- This removes the need for manual configuration management in the endpoints.
>
>#### **2. Factory for Providers**
>- The `ProviderFactory` uses the injected `AppConfig` to dynamically instantiate providers.
>- The factory abstracts away the complexity of creating and configuring provider instances.
>
>#### **3. Injecting Providers via DI**
>
>- The factory itself can be injected into endpoints using FastAPI’s DI system.
>- Example:
>    `@router.post("/") async def query_api(factory: ProviderFactory = Depends(get_provider_factory)):     providers = factory.create_providers()     ...`
>    
>#### **Combined Flow**
>1. FastAPI resolves `get_config` to provide the `AppConfig`.
>2. The `ProviderFactory` is instantiated with `AppConfig` to create providers.
>3. Providers are injected into endpoints or services as needed.

Couple of updates need to be made:
1. **~={cyan}Dependency Injection=~**: Inject pre-configured `ProviderFactory` objects instead of instantiating them in endpoints.
2. **~={cyan}Factory Pattern=~:** Use a fully centralized `ProviderFactory` class instead of partially implemented dynamic instantiation.



---

#backend #fastapi #webapp #multiquery #research #development #pydantic #configs #dependencyinjection #fastapi #python #importlib
