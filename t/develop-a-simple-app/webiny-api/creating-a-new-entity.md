# Entities - Classes

Entities are basically the foundation of every app. They help you define your data models, business logic and processes.

In this section, we will create a few entities for our simple OpenLibrary application. Since it will store a list of books, with its authors and categories in which they belong, basically we'll need to define three entities:

1. Book
2. Author
3. Category

_\[SCHEME\]_

## Create files

To keep things organized, in our project's `api/src/app` folder, let's create `entities` folder. In it, we will create three files that will represent needed entities. Once created, we should have the following structure:

```text
.
├── api
│   └── src
│       ├── app
│       │   ├── entities
│       │   │   ├── author.entity.js
│       │   │   ├── book.entity.js
│       │   │   └── category.entity.js
```

{% hint style="info" %}
Although not necessary, it's practical to name entity files with `.entity.js` suffix, so that further searching for files is easier.
{% endhint %}

## Define entity classes

Defining entities is easy. We created our own entity layer or in other words an ORM, with a simple syntax and powerful set of features. At this point, basic usage will be shown, but if you'd like to learn more, please visit our [Entity](../../../reference-manual/components/entity-layer/) section.

To define our three entities, let's examine the following three files:

{% code-tabs %}
{% code-tabs-item title="author.entity.js" %}
```javascript
import { Entity } from "webiny-api";

class Author extends Entity {
    constructor() {
        super();
        this.attr("firstName").char().setValidators("required");
        this.attr("lastName").char().setValidators("required");
    }
}

Author.classId = "OpenLibrary_Authors";

export default Author;
```
{% endcode-tabs-item %}

{% code-tabs-item title="category.entity.js" %}
```javascript
import { Entity } from "webiny-api";

class Category extends Entity {
    constructor() {
        super();
        this.attr("name").char();
    }
}

Category.classId = "OpenLibrary_Categories";

export default Category;
```
{% endcode-tabs-item %}

{% code-tabs-item title="book.entity.js" %}
```javascript
import { Entity } from "webiny-api";
import Category from "./category.entity";
import Author from "./author.entity";

class Book extends Entity {
    constructor() {
        super();
        this.attr("title").char().setValidators("required");
        this.attr("year").int();

        this.attr("author").entity(Author).setValidators("required");
        this.attr("category").entity(Category);
    }
}

Book.classId = "Book";
Book.tableName = "OpenLibrary_Books";

export default Book;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

There are a few importants parts here:

1. Entity classes must extend base `Entity` class, imported from `webiny-api`.  
2. Each entity consists of attributes. For example we used `char` attribute for first name and last name in `Author` entity. We also used `int`for year attribute in `Book` entity, and finally `entity` attribute for linking books with authors and categories.  A list of all available attributes can be found in [reference manual](../../../reference-manual/components/entity-layer/attributes.md#attributes-list). 
3. Continuing with the 2nd point, we didn't specify the `id` attribute. This and a few other useful attributes \(eg. `createdOn`, `updatedOn`, `savedOn`\) will be automatically included for you, which was achieved immediately by extending the base `Entity` class. You can also visit the reference manual to take a look at the complete list of [automatically included attributes](../../../reference-manual/components/entity-layer/attributes.md#automatically-included-attributes). 
4. We also set `required` validators for a few attributes. More thorough information on attribute validators can also be found in [reference manual](../../../reference-manual/components/entity-layer/attributes.md#validators). 
5. Finally, each entity needs to have a `classId`static property which is used for better entity differentiation and some other internal handling. We also added `tableName`, which obviously determines the table name in our MySQL database.

## Register entities

After we've defined our entity classes, the next step is to register them to our app.

Entities are registered using the central `api` object \(imported from `webiny-api`\), which, apart from registering entities, also offers other useful options, like registering GraphQL operations, services, holds a list of used apps etc.

{% hint style="info" %}
To learn more about the `api` object, please visit the [reference manual](../../../reference-manual/webiny-api/webinyapi-object.md).
{% endhint %}

So to register entities, we can simply open our app file, located in `api/src/app/myApp.js`, and use `app.entities.addEntityClass` method, like in the following example:

{% code-tabs %}
{% code-tabs-item title="myApp.js" %}
```javascript
// @flow
import Book from "./entities/book.entity";
import Category from "./entities/category.entity";
import Author from "./entities/author.entity";

export default () => {
    return {
        init({ app }: Object, next: Function) {
            // Entities registration
            app.entities.addEntityClass(Book);
            app.entities.addEntityClass(Category);
            app.entities.addEntityClass(Author);
            
            // Proceed to next app.
            next();
        }
    };
};
```
{% endcode-tabs-item %}
{% endcode-tabs %}

You might be asking yourself why do we need to additionally register entities. The action itself does not do anything special, it just adds the classes to an internal list. But the list itself can be useful in later stages. For example, it's being used by the security module, to enable admins to manage permissions for all registered entities. More information on security will be provided in one of the following sections.

Now that we have our entities registered, we have to prepare our database - create MySQL tables. Although you could do this by hand, in this guide, we will show you the easier way - using MySQL Tables system component.

