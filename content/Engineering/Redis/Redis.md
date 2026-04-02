# Data Structure

# Evection Policy
- To determine what to do when the instance is full of memory
- Default policy: `volatile-lru`
- `noeviction` -> new values is not stored

I note the policy name by prefix and postfix to remember

Prefix to determine apply scope for keys with only `expired` or not
- `allkeys` -> all keys
- `volatile` -> keys with expired set to true

Postfix to determine the eviction rule
- `lru` -> remove least recently use keys
- `lfu` -> remove least frequently use keys
- `random` -> remove randomly duh uh
- `ttl` (only for `volatile`): remove keys with shortest TTL

Practice: should keep the database large enough to store all the data

Use case:
- user session -> `volatile-lru 
- generic cache -> `allkeys-*`
