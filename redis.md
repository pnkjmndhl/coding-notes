### introduction
- key-value, in-memory, NoSQL database
- simple data formats
  - no database schema
  - no complex data models
- in memory
  - no hard drives, and no delay in data access
- MySQL and PostgreDB cannot compete with the performance of Redis
- however, in-memory data may be lost
- usually used as an auxiliary system to improve performance
- 
### installing redis
- `redis.io`
- redis server `Redis`
  - to start a server `redis-server`
  - all command logics runs here
- redis client
  - to start a client `redis-cli`
  - gateway to the server
  - only useful to test commands in the server
  - terminal CLI is a `gate` to the redis server

