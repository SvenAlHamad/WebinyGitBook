# The basics

## Files and folders

Let's take a look at the initial organization of files and folders inside our `api` folder. 

```text
.
├── api
│   ├── node_modules
│   ├── package.json
│   ├── src
│   │   ├── app
│   │   │   ├── database.js
│   │   │   ├── index.js
│   │   │   ├── middleware.js
│   │   │   ├── myApp.js
│   │   └── express
│   │       └── index.js
```

All of the files and folders we will be creating over the next couple of sections will be placed in the`api/src/app` folder. Note that Webiny does not enforce any particular organization or naming conventions for files and folders.

## How it works

It's important to recognize that Webiny API is basically an [express middleware](https://expressjs.com/en/guide/using-middleware.html). For now, only note that initialization of a new express app and middleware registration can be found in the `api/src/app/index.js` file. If you're already familiar with Express, the code should be pretty straight-forward - it basically just mounts Webiny API middleware on `/graphql` path.

More in-depth information on how it works, different options and configurations can be found in the [reference manual](../../../reference-manual/webiny-api/).

{% hint style="info" %}
Once initialized, Webiny project will already be configured and ready for local development. You can later tweak different parameters to your needs.
{% endhint %}

## Next steps

We've taken a brief look on the folder structure and initialization process. Now that we know the basics, let's move to the actual app development. 

In the next section, we will create our first entities, which are basically the foundation of every app.

