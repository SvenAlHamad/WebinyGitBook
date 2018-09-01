# Entities - MySQL Tables

By default, Webiny CMS is used with MySQL database, which means for each entity, a corresponding table must be present in the database.

Although you can create these by hand, you can also do it using built-in MySQL Tables system component, which will enable you to define tables in a declarative and maintainable way. Basically, it lets you create a simple class, in which you can define all of the columns and indexes. Once defined, you can use the Sync Tool to create tables or sync the structure with a real database.

{% hint style="info" %}
To learn more about MySQL Tables, be sure to visit the [reference manual](../../../reference-manual/components/mysql-tables/).
{% endhint %}

## Create files

For starters, let's create another folder in our project, named `tables`. In the same way as in the [previous](creating-a-new-entity.md) section, we will create three files that will represent needed tables. Once created, we should have the following structure:

```text
.
├── api
│   └── src
│       ├── app
│       │   ├── entities
│       │   │   ├── author.entity.js
│       │   │   ├── book.entity.js
│       │   │   └── category.entity.js
│       │   ├── tables
│       │   │   ├── author.mysql.js
│       │   │   ├── book.mysql.js
│       │   │   └── category.mysql.js
```

{% hint style="info" %}
Although not necessary, it's practical to name table files with `.mysql.js` suffix, so that further searching for files is easier.
{% endhint %}

## Define tables

Since our entities are simple, our tables will be simple too. Let's examine the following code:

{% code-tabs %}
{% code-tabs-item title="author.mysql.js" %}
```javascript
import Table from "./table.mysql";

class AuthorTable extends Table {
    constructor() {
        super();
        this.column("firstName").varChar(100);
        this.column("lastName").varChar(100);
    }
}

AuthorTable.setName("OpenLibrary_Authors");

export default AuthorTable;
```
{% endcode-tabs-item %}

{% code-tabs-item title="category.mysql.js" %}
```javascript
import Table from "./table.mysql";

class CategoryTable extends Table {
    constructor() {
        super();
        this.column("name").varChar(100);
    }
}

CategoryTable.setName("OpenLibrary_Categories");

export default CategoryTable;
```
{% endcode-tabs-item %}

{% code-tabs-item title="book.mysql.js" %}
```javascript
import Table from "./table.mysql";

class BookTable extends Table {
    constructor() {
        super();
        this.column("title").varChar(100);
        this.column("year").smallInt();
        this.column("author").char(24);
        this.column("category").char(24);
    }
}

BookTable.setName("OpenLibrary_Books");

export default BookTable;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

We can see that we used a few basic column types, `varChar(100)` for first and last name, `integer` for year, and in `BookTable`, we used `char(24)` for author and category, because our entity layer uses 24-character \(MongoDB-style\) IDs, instead of regular auto-incremented integers.

KAKO OBJASNITI TABLE.MYSQL DIO ? INSTALL PROCEDURA TREBA OVDJE ?

Now that we have covered table creation and our database is ready, let's move on to exposing basic CRUD operations via API.



