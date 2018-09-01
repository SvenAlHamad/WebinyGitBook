# Entity pool

### Entity pool

Entity pool is simply put a local entity cache, which by default holds entities in memory until the process ends.

Once an entity has been created or loaded from database, it will immediately be added to it. Then in later stages, when trying to load entities using [findById](untitled.md#findbyid), [findByIds](untitled.md#findbyids) or [find](untitled.md#find) method, entities will be returned from entity pool if possible, thus preventing additional database queries.

### Custom Entity Pool

By default, entities will be held in memory until the process has finished. If this is not appropriate, custom entity pool can be implemented. One example is implementing a per-request entity pool, in which entities would be held in it while the request is active. Once finished, pool would be emptied.

You can assign a custom entity pool using [pool](configuration-1.md#pool) static class property.

