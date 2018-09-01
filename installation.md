# Installation

## Prerequisites

Before installing Webiny, make sure you have installed the following:

1. NodeJS **v8.0.0** or higher
2. yarn **v1.3.0** or higher
3. MySQL **v5.7** or higher

## Install webiny-cli

Before creating a Webiny project, you have to install Webiny CLI. If you've already installed it, skip to the next step.

You can do this by executing the following command in your terminal \(installs the tool globally on your system\):

`$ yarn global add webiny-cli`

To make sure everything was correctly installed, run the following command to get the current version of the CLI:

`$ webiny -v  
$ v2.0.0`

## Create project

To start working with Webiny, we must set up a new project, which will consist of three simple steps.

### 1. Create a new project using Webiny CLI

To create a new project, we will use the Webiny CLI tool. In terminal, type in the following commands:

`$ cd /your/dev/folder  
$ webiny create FooProject`

Once finished, this will create a new folder for your project and prepare all necessary files. You should have the following folder structure:

```text
. 
├── api
└── client
```

### 2. Setup MySQL database connection parameters

The next step is to configure the MySQL connection parameters, which are located in the following file: `/api/src/app/database.js`.

### 3. Build

Webiny is made up of two parts - client and API. Because of this, we must build both sides.

#### Client: 

`$ cd /client & yarn develop`

#### API

`$ cd /api & yarn develop`

{% hint style="info" %}
Running the API development session for the first time will trigger the API installation process, which will set up the database and create admin user account.
{% endhint %}

## Login to admin UI

Using automatically generated credentials, you can now login into the admin UI. 

Open the following link in your browser: [http://localhost:8060/admin/login](http://localhost:8060/admin/login), and use the following credentials to log in for the first time:

```text
Username: admin@webiny.com
Password: 12345678
```

![Admin UI login screen](.gitbook/assets/image%20%288%29.png)

### Further reading

Now that you have initialized your first project, you can continue with our [CMS](webiny-cms-basics/) section, in which you will learn how it works and how to create categories, pages, use widgets and more!

If you are also interested in custom development, you can also visit our [Guides](t/) section.

