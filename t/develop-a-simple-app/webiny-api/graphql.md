# GraphQL - Add Operations to Schema

In order for client apps to be able to eg. create or read books, we must expose related GraphQL operations.

Webiny API has a GraphQL layer implemented so exposing operations is a simple and automatic process. Like in the previous section, we'll do it in our app file \(`api/src/app/myApp.js`\) using the central `api` object, via the `app.graphql.schema` method \(starting on line 15\):

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
            // Entities registration.
            app.entities.addEntityClass(Book);
            app.entities.addEntityClass(Category);
            app.entities.addEntityClass(Author);
            
            // Expose GraphQL operations.
            app.graphql.schema(schema => {
                schema.addEntity(Book);
                schema.addEntity(Category);
                schema.addEntity(Author);
            });
            
            // Proceed to next app.
            next();
        }
    };
};
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Behind the scenes, this will create all of the needed CRUD operations for each entity, so you don't have to do it by yourself. To see the changes in the GraphQL schema and get a better feel, we can open the [graphiql](https://github.com/graphql/graphiql) tool, by opening `{base_url}/graphql` \(eg. `http://localhost:9000/graphql`\) in the browser. Once opened, if we search for all "Book" related queries and mutations, we should get the following list:

![CRUD methods are automatically created.](../../../.gitbook/assets/image%20%286%29.png)

Now that we have the list, we could for example try to execute a simple `listBooks` query. But, you would soon find found that instead of actual data, a security-related error would occur:

![Executing base listBooks query results with an security error.](../../../.gitbook/assets/image%20%282%29.png)

This is because in order to be able to read `Book` entities and to execute `listBooks` operation, we must make apply certain changes in the built-in security module, which is topic of the [next](security.md) section.

