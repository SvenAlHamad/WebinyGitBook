# api Object

`api` object is the central object that represents completely initialized Webiny API. Note that it is **singleton**, which means each time you import it in your code, you will receive the exact same instance.

{% hint style="info" %}
To import `api` object, use `import { app } from "webiny-api";`.
{% endhint %}

Apart from offering a few useful methods \(eg. already seen `middleware` method for creating an Express middleware\), `api` object also contains the following:

* a complete configuration parameters used upon initialization
* reference to the current `request` object, so you can access it eg. within your entities or services

But there is more!

Webiny API also embraces the concept of **apps**. Once an app is used in a project, it can affect or expand the system by:

* registering additional entities, services and GraphQL operations
* attaching event handlers or defining new system events to implement its own custom logic



