>[!note]
>[MongoDB Fundamentals](https://www.mongodb.com/docs/manual/faq/fundamentals/#faq--mongodb-fundamentals)

**~={green}Collections=~** are analogous to a Relational DB table
~={green}**Documents**=~ are analogous to Records/Rows in a Relational DB table
### Default Databases
- **`admin` Database:** This database is crucial for administrative operations. It stores user authentication information, roles, and other administrative settings. **It's essential for managing your MongoDB server and should NOT be deleted.**  
- **`config` Database:** In a sharded cluster (a more advanced MongoDB setup for handling large datasets), the `config` database stores metadata about the cluster's configuration, including shard information and chunk distribution. **If you're not using sharding (which is typical for local development), this database is generally not actively used but it's still best to leave it alone.** Deleting it could cause issues if you later decide to implement sharding.
- **`local` Database:** This database is used for local server information, such as oplog (operation log) data, which is important for replication. **For single-server local development, this database is also not strictly necessary but it's best to leave it untouched.** Deleting it won't cause immediate problems in a simple setup, but it's a core part of MongoDB's internal workings.

>[!CAUTION]
>It's **strongly recommended NOT to delete** the `admin`, `config`, or `local` databases. They are part of MongoDB's internal structure and are used for various functionalities, even in a local development environment. Deleting them could lead to unexpected behavior or issues if you later decide to use more advanced MongoDB features.

