### Minimal Schema Based on PoC
Here’s a streamlined schema for the **Proof of Concept**:

| **Field**      | **Type**        | **Description**                                    |
| -------------- | --------------- | -------------------------------------------------- |
| `id`           | `string`        | Unique identifier for the context.                 |
| `element`      | `array<string>` | Categories/tags that describe the context.         |
| `data`         | `string`        | The actual information stored in the context.      |
| `created_date` | `datetime`      | Timestamp indicating when the context was created. |
### Recommended Schema for Scalability
To future-proof the design while keeping it simple, I recommend adding two lightweight fields: `title` and `updated_date`.

| **Field**      | **Type**        | **Description**                                              |
| -------------- | --------------- | ------------------------------------------------------------ |
| `id`           | `string`        | Unique identifier for the context.                           |
| `element`      | `array<string>` | Categories/tags that describe the context.                   |
| `data`         | `string`        | The actual information stored in the context.                |
| `created_date` | `datetime`      | Timestamp indicating when the context was created.           |
| `updated_date` | `datetime`      | Timestamp indicating the last time the context was modified. |
| `title`        | `string`        | Short, human-readable summary of the context.                |
### Example Schema JSON
```json
{
  "_id": "unique_context_id",
  "user_id": "user_123",  // Optional: Useful if supporting multiple users
  "title": "Health Goals",
  "element": ["health", "fitness", "diet"],
  "data": "I prefer a Mediterranean diet and avoid gluten.",
  "embedding": [0.123, -0.456, 0.789],  // Optional: For semantic search
  "created_at": "2024-12-22T10:00:00Z",
  "updated_at": "2024-12-22T10:00:00Z"
}
```

---
## ~={red}IMPORTANT: Future Proofing for Semantic RAG=~
>[!info]- How "Elements" fit in Semantic-Based RAG
>**In Semantic-Based RAG**
>- Instead of relying on exact tag matches, **embeddings** are used to represent the semantic meaning of both the query and the stored contexts.
>- **Elements can still provide structure**:
>	- They serve as high-level descriptors for grouping or filtering contexts before embedding-based similarity searches.
>	- Example: A user query is compared against embeddings for documents labeled with specific elements (e.g., only "health-related" documents).
>
>**How "Element" Can Translate**
>- **Option 1: Pre-Semantic Filtering with Elements**
>	- Use **elements** to narrow down the pool of contexts before performing the semantic search.
>	- A query related to "diet" first filters out documents labeled with unrelated elements like "finance."
>	- The remaining contexts undergo semantic similarity comparison.
>	- Reduces computation by limiting the number of embeddings compared.
>
>- **Option 2: Embedding Elements as Metadata**
>	- Assign each **element** its own embedding vector, representing its semantic meaning.
>	- During semantic search, the **query embedding** can prioritize documents associated with elements that semantically align with the query.
>	- If the query is _"healthy meal plans,"_ it might semantically align with the "diet" and "health" element embeddings, boosting the relevance of documents tagged with these elements.
>
>- **Option 3: Elements as Contextual Boosters**
>	- Use **elements** to boost or influence semantic similarity scores
>		- If a query or context is associated with an element, apply a weight or bias to prioritize its relevance.
>		- Example: Query embedding matches with multiple contexts, but those labeled with "health" are given a higher score because the query also mentions "fitness goals."
>
>**Evolving the Role of Elements**
>- In **tag-based RAG**, elements are explicit, user-defined tags.
>- In **semantic-based RAG**, elements act as:
>	- **Pre-filters**: Limiting the search space.
>	- **Metadata**: Enhancing semantic scoring.
>	- **Organizational Layers**: Allowing manual overrides or query constraints.
>
>**Benefits of Retaining Elements in Semantic-Based RAG**
>- **Improved Precision**
>	- Combining **elements** with semantic similarity provides more precise results, especially when the database grows.
>- **Hybrid Approach**
>	- Elements offer a simple, interpretable layer for users, while embeddings handle complex, nuanced relationships.
>- **Scalability**
>	- As new elements are added, they enrich the organizational structure without impacting embedding-based retrieval.
>- **Explainability**
>	- Elements provide an easy way to explain why certain contexts were retrieved (e.g., _"This document was prioritized because it matches your query and falls under the 'health' element."_).

I want to store it in JSON format. I also want it to be scalable and future proof it with different RAG implementations. Design the schema to support **semantic-based RAG** so we can transition away from tag-based RAG.

This means you need to include an **EMBEDDING** field with a vector value
```json
{
  "_id": "unique_context_id",
  "title": "Health Goals",
  "element": ["health", "diet"],
  "data": "I prefer a Mediterranean diet and avoid gluten.",
  "embedding": [0.123, -0.456, 0.789]  // Example vector
}
```

BUT you can include this field later. Since you're using NoSQL, you can always change the schema later.
Example command to add "embedding" field:
```python
db.contexts.update_many({}, {"$set": {"embedding": []}})
```

