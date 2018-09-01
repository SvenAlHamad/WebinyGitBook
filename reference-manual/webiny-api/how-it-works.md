# How it works

On a high-level, Webiny API is enabled by simply using Webiny API middleware on a new or even existing Express app. if you're already familiar with [Express](https://expressjs.com/) and the concept of [middleware](https://expressjs.com/en/guide/using-middleware.html), the following section should be pretty straight-forward.

{% hint style="info" %}
Once created, Webiny project will already be configured and ready for local development. You can then tweak different parameters to your needs.
{% endhint %}

Following the previously shown [project structure](../../t/develop-a-simple-app/__code-structure.md), if we open the `api` folder, we should have the following:

```text
.
├── README.md
├── api
│   ├── .babelrc
│   ├── package.json
│   └── src
│       ├── app
│       │   ├── database.js
│       │   ├── index.js
│       │   ├── middleware.js
│       │   └── myApp.js
│       └── express
│           └── index.js
```

For now, let's open the `api/src/app/index.js` file, in which an Express app is set:

```javascript
import express from "express";
import path from "path";
import bodyParser from "body-parser";
import cors from "cors";
import setupProject from "./middleware";

export default async () => {
    const webiny = await setupProject();

    const app = express();

    if (process.env.NODE_ENV === "development") {
        const morgan = require("morgan");
        app.use(morgan("tiny"));
    }

    app.use(cors());
    app.use("/storage", express.static(path.join(__dirname, "/../../storage")));
    app.use(
        "/graphql",
        bodyParser.json({ limit: "50mb" }),
        webiny.middleware(({ securityMiddleware, graphqlMiddleware }) => [
            securityMiddleware(),
            graphqlMiddleware(),
        ])
    );

    return app;
};
```

Apart from registering standard middleware like eg. [cors](https://github.com/expressjs/cors), notice the Webiny API middleware, mounted on `/graphql` path \(line 19\), right after [bodyParser](https://github.com/expressjs/body-parser). It's been created using the `middleware` method from `webiny` object, an instance of  `WebinyAPI` class, which is the central object that basically represents initialized Webiny API. More information about its purposes and structure will be presented in the [next](webinyapi-object.md) section.

For now, the main thing to note is that created Webiny API middleware also has its own built-in middleware mechanism, and that by default it provides two basic ones:

1. `securityMiddleware` - responsible for security and although optional, it's strongly recommended to  have it enabled, before the `graphqlMiddleware`
2. `graphqlMiddleware` - required, it has to be here in order for GraphQL server to work.

You can then insert your own custom middleware at any spot, even after `grapqlMiddleware`. For example, you could append a custom API response cache middleware.

{% hint style="info" %}
Presented file is actually imported and executed inside `api/src/express/index.js`file, but because of async operations and better code readability, it has been moved to a separate file.
{% endhint %}

Let's continue by taking a closer look at the `WebinyAPI` object.

