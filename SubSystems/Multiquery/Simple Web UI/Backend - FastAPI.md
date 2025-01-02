### **Plan for FastAPI Backend**
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
### **Step 1: Install Required Dependencies**
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

---
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
## Settings Configs

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

**`get_config` Function**:
- This function acts as a **dependency provider** for the configuration object.
- It simply returns the pre-loaded `config` object from `app.py`.
**Dependency Injection in `query_api`**:
    - FastAPI’s `Depends(get_config)` automatically injects the `config` object into the `query_api` function.
**Modular Reuse**:
    - `get_config` can now be reused across all endpoints in your application without requiring repetitive imports or global variables.

So the configurations are now global and mapped to Pydantic BaseModel Configs found in `multiquery -> core -> config.py`



---

#backend #fastapi #webapp #multiquery #research #development #pydantic #configs
