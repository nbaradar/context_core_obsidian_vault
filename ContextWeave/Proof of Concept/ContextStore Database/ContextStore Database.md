# Conceptual Design
Here are the pieces involved in the ContextStore:
### Context
- Each piece of data in the database is a "context." The actual data (or document) stored in the database represents a single, structured meaningful piece of information. 
- Each context can be associated with one or more elements
**Example**: "I prefer a Mediterranean diet and avoid gluten."
### Element
- This is the "label" or "category" for each context stored in the database. It organizes different contexts into logical groups.
- Think of them as building blocks that describe the nature of contexts. This enables efficient retrieval and grouping of contexts
**Example**: "health", "finance", "personality"

# Approach
How are you going to store this data?

**NoSQL** should be used for Flexibility. Could switch to relational database later for performance gains
For this reason, I'm going with **~={green}MongoDB=~** as my DB for POC. Notes found [[MongoDB|here]]

Also need to design a [[Schema Design|Schema]] that is simple yet scalable. 

%% Begin Waypoint %%
- [[Random Old GPT response]]
- [[Schema Design]]

%% End Waypoint %%

