# Options

Entity component has a couple of static class properties, that offer a way to set additional options. The following is a list of all static class properties that can be used.

### `classId`

Each entity class must have a classId. Once defined, it can be used to identity entity type without checking the name of the actual class. It is used internally by the Entity component \(can be even stored in the database in some cases\), but can also be used while developing business logic if needed.

**Example**

```javascript
import { Entity } from "webiny-entity";

class User extends Entity {
    constructor() {
        super();
        this.attr("firstName").char();
        this.attr("lastName").char();
    }
}

// classId doesn't have to be the same as the name of the actual class.
User.classId = "SecurityUser";
```

### `driver`

In order to actually be able to store and read data from database, a driver must be set. Use this class property to set a new instance of configured driver. Currently Webiny hosts two official drivers - [MySQL]() and [Memory]().

{% hint style="info" %}
The most convenient way to set a driver is to first import and extend the base Entity class. Once the desired driver is assigned, export the class and extend it when defining actual entities.

This way, you won't have to assign the driver to each Entity class separately.
{% endhint %}

**Example**

{% code-tabs %}
{% code-tabs-item title="baseEntity.js" %}
```javascript
import { Entity as BaseEntity } from "webiny-entity";
import { MemoryDriver } from "webiny-entity-memory";

class Entity extends BaseEntity {}
Entity.driver = new MemoryDriver();
​
export default Entity;
```
{% endcode-tabs-item %}

{% code-tabs-item title="user.entity.js" %}
```javascript
import Entity from "./baseEntity.js";

class User extends Entity {
    // ...
}

User.classId = "User";
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### `pool`

Entity pool is basically an entity cache, which prevents redundant database calls.  By default, loaded entities will be stored in memory, and flushed once the process has ended. 

{% hint style="info" %}
Visit [entity pool]() section to learn more about it.
{% endhint %}

This property can be used to assign a different entity pool if needed.

**Example**

{% code-tabs %}
{% code-tabs-item title="baseEntity.js" %}
```javascript
import { Entity as BaseEntity } from "webiny-entity";

class Entity extends BaseEntity {}
Entity.pool = new CustomEntityPool();
​
export default Entity;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### `crud`

Exposes few useful CRUD options. Assigned object has the following structure:

* `logs` **boolean** Automatically includes `createdOn`, `updatedOn` and `savedOn` [date](attributes.md#date) attributes in each entity, and updates values accordingly. `savedOn` is updated on both [create and update](untitled.md#save) operations.
* `delete` **object** Provides delete operation options.
  * `soft` **boolean** Enables soft delete - each entity will receive `deleted` [boolean](attributes.md#boolean) attribute, which will be set to `true` when entity is deleted, instead of actually deleting the record in the database. Entity component also handles further querying, meaning it will append necessary filters automatically.

**Example**

```javascript
import { Entity as BaseEntity } from "webiny-entity";

class Entity extends BaseEntity {}

Entity.crud = {
    logs: true,
    delete: {
        soft: true
    }
};
​
export default Entity;
```

