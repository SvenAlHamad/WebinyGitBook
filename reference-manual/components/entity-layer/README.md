# Entity

Entity component, as the name already suggests, provides a way to work with entities that are part of your business logic. The component can be categorized as both [ORM and ODM](https://en.wikipedia.org/wiki/Object-relational_mapping), because essentially it can work with any type of database, be it SQL, NoSQL or even browser's local storage if needed. It's just a matter of using a specific driver, and you're good to go.

Webiny currently hosts two official drivers - [MySQL](https://github.com/webiny/webiny-js/tree/master/packages-utils/webiny-entity-mysql) and [Memory](https://github.com/webiny/webiny-js/tree/master/packages-utils/webiny-entity-memory) drivers. Additional drivers may be added \(eg. PostgreSQL or MongoDB\) as the need arises in the near future.

To check out latest changes and current state of the component, please visit the official [GitHub repo](https://github.com/Webiny/webiny-js).

## Quick Example

In general, the first step of defining a new entity is to extend a base `Entity` class from `webiny-api` package, and then define attributes in class `constructor`. To quickly get an impression on how it works, please consider the following examples:

{% code-tabs %}
{% code-tabs-item title="user.entity.js" %}
```javascript
import { Entity } from "webiny-api";
import Company from "./company.entity.js";

class User extends Entity {
    constructor() {
        super();
        this.attr("email")
            .char()
            .setValidators("required,email")
            .onSet(value => value.toLowerCase().trim());

        this.attr("password")
            .password()
            .setValidators("required");
            
        this.attr("firstName").char();
        this.attr("lastName").char();
        this.attr("age").integer();
        this.attr("enabled").boolean();
        
        this.attr("company")
            .entity(Company)
            .setValidators("required");
    }
}

User.classId = "User";
export default User;
```
{% endcode-tabs-item %}

{% code-tabs-item title="company.entity.js" %}
```javascript
import { Entity } from "webiny-api";

class Company extends Entity {
    constructor() {
        super();
        this.attr("name").char();
        this.attr("type").char().setValidators("in:tourism:it:seo:trading");
        this.attr("enabled").boolean();
    }
}

Company.classId = "Company";

export default Company;

```
{% endcode-tabs-item %}

{% code-tabs-item title="createUser.js" %}
```javascript
import User from "./user.entity.js";

const data = {
  email: "john.doe@webiny.com",
  password: "12345678",
  firstName: "John",
  lastName: "Doe",
  age: 30,
  enabled: true,
  company: { name: "A test company", type: "it" }
};

const user = new User();
user.populate(data);
await user.save();
```
{% endcode-tabs-item %}

{% code-tabs-item title="getUser.js" %}
```javascript
import User from "./user.entity.js";
​
const user = await User.findOne({query: {email: "john.doe@webiny.com"}});
console.log(user.firstName); // John

const company = await user.company;
console.log(company.name); // A test company
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Shown examples are demonstrating basic usage of the Entity component. If you would like to learn more, feel free to continue with the [next](attributes.md) section, in which we will talk more about all of the available attributes and its options.

