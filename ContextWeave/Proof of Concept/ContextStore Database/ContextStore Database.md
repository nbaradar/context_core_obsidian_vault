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

---
# Approach
How are you going to store this data?

**NoSQL** should be used for Flexibility. Could switch to relational database later for performance gains
For this reason, I'm going with **~={green}MongoDB=~** as my DB for POC. Notes found [[MongoDB|here]]

Also need to design a [[Schema Design|Schema]] that is simple yet scalable. 

---
# Database Design
```bash
Database: ContextStore
  ├── Collection: contexts
  └── Collection: elements (optional)
```
**`contexts`** (required): Stores the core data for each context.
**`elements`** (optional): Provides structure and validation for elements.

Example Schema
```json
{
  "_id": "unique_context_id",
  "title": "Health Goals",
  "element": ["health", "fitness", "diet"],
  "data": "I prefer a Mediterranean diet and avoid gluten.",
  "created_at": "2024-12-22T10:00:00Z",
  "updated_at": "2024-12-22T10:00:00Z"
}
```

If you simply omit the `_id` field when inserting a document, MongoDB will automatically generate a unique `ObjectId` for you.

For the `created_at` field, you can use `$setOnInsert` and `$currentDate`
```javascript
db.myCollection.insertOne({
  "user_id": "user_123",
  "title": "Health Goals",
  // ... other fields
  $currentDate: { created_at: { $type: "date" }, updated_at: { $type: "date" } } // Set both on insert
});
```

For the `updated_at` field, you can auto-generate timestamps using `$currentDate`
```javascript
db.myCollection.updateOne(
  { _id: ObjectId("6585c54c7b8b8b8b8b8b8b8b") }, // Replace with the actual _id
  { $currentDate: { updated_at: true } }
);
```

#### Elements for POC
- **Health**: Covers fitness, diet, and wellness.
	- `health`, `fitness`, `diet`
- **Finance**: Covers budgeting and investments.
	- `finance`, `budget`, `savings`, `investing`, `debt`, `retirement`, `taxes`
- **Personal Development**: Covers hobbies, learning, and self-improvement.




%% Begin Waypoint %%
- [[Random Old GPT response]]
- [[Schema Design]]
- **Test Data**
	- [['Finance' contexts]]
	- [['Health' contexts]]
	- [['Personal Development' Data]]

%% End Waypoint %%

