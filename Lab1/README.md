# Lab1 - Loopback

The apiconnect cli generates a dressed down version of a Loopback application. To get the full features of the Loopback cli generator, you have to use the `lb` cli directly. 

See: https://developer.ibm.com/apiconnect/create-your-api/

## Loopback
Strongloop was founded in 2012 by Node.js experts Bert Belder, Ben Noordhuis, and Al Tsang. IBM acquired Strongloop in 2015. Loopback is an open source Node.js API framework built on top of Node.js and Express.js by top contributors to open source Node.js and Express.js. 

See: https://loopback.io/doc/en/lb3/

## API Connect
API Connect is the API Management framework built by IBM. API Connect integrates with Loopback and is available as an API Connect service on IBM Cloud.

See: https://developer.ibm.com/apiconnect/getting-started

## Open API Initiative (OAI)
The OpenAPI Initiative (OAI) is an open governance structure under the Linux Foundation, focused on creating, evolving and promoting a vendor neutral description format.

SmartBear Software donates the Swagger Specification directly to the OAI as the basis of this Open Specification.

See: https://www.openapis.org/

## Swagger
Swagger is built by SmartBear Software.

See: https://swagger.io/specification/

# Lab1

1. Create a Loopback application

    * Create a Loopback v3 application with: 
        * name `apic-api`, 
        * version `3.x` and 
        * template `empty-server`, 

    ```
    $ apic loopback
    ? What's the name of your application? apic-api
    ? Enter name of the directory to contain the project: apic-api
    ? Which version of LoopBack would you like to use? 3.x (current)
    ? What kind of application do you have in mind? empty-server
        Created package.json
        Created server
        Created server/boot
        Created server/boot/root.js
        Created server/config.json
        Created server/datasources.json
        Created server/middleware.development.json
        Created server/middleware.json
        Created server/model-config.json
        Created server/server.js
    ...and a lot more

    Updating swagger and product definitions
    Created /apic-api/definitions/apic-api.yaml swagger description
    Created apic-api-product.yaml product definition [apic-api:1.0.0]

    Next steps:

    Change directory to your app
        $ cd apic-api

    Create a model in your app
        $ apic create --type model

    Compose your API, run, manage, enforce and deploy it with API Connect
        $ apic edit

    Run the app
        $ apic start
    ```

    * Review the generated YAML files in the `definitions` folder. You will find a `swagger 2.0` file. The product YAML contains meta-data for the API Connect management service, like product version, visibility and plan properties. 

2. Add a model,

    * Add an `PersistedModel`, `common` object model `Post` to the Loopback application. Add properties for 
        * `id` (number, required), 
        * `title` (string, required),
        * `subtitle` (string),
        * `publicationDate` (date, required),
        * `text` (string, required),
        * `userId` (number, required)

    ```
    $ cd apic-api
    $ apic create --type model
    Warning: Found no data sources to attach model. There will be no data-access methods available until datasources are attached.
    
    ? Enter the model name: Post
    ? Select model's base class PersistedModel
    ? Expose Post via the REST API? Yes
    ? Custom plural form (used to build REST URL): 
    ? Common model or server only? common
    Let's add some Post properties now.

    Enter an empty property name when done.
    ? Property name: id
    invoke   loopback:property
    ? Property type: number
    ? Required? Yes
    ? Default value[leave blank for none]: 

    Let's add another Post property.
    Enter an empty property name when done.
    ? Property name: title
    invoke   loopback:property
    ? Property type: string
    ? Required? Yes
    ? Default value[leave blank for none]: 

    Let's add another Post property.
    Enter an empty property name when done.
    ? Property name: subtitle
    invoke   loopback:property
    ? Property type: string
    ? Required? No
    ? Default value[leave blank for none]: 

    Let's add another Post property.
    Enter an empty property name when done.
    ? Property name: publicationDate
    invoke   loopback:property
    ? Property type: date
    ? Required? Yes
    ? Default value[leave blank for none]: 

    Let's add another Post property.
    Enter an empty property name when done.
    ? Property name: text
    invoke   loopback:property
    ? Property type: string
    ? Required? Yes
    ? Default value[leave blank for none]: 

    Let's add another Post property.
    Enter an empty property name when done.
    ? Property name: userId
    invoke   loopback:property
    ? Property type: number
    ? Required? Yes
    ? Default value[leave blank for none]: 

    Let's add another Post property.
    Enter an empty property name when done.
    ? Property name: 
    Done running LoopBack generator

    Updating swagger and product definitions
    Created /apic-api/definitions/apic-api.yaml swagger description
    ```

    * Loopback added a definition for the Post model with access for `Posts` resource endpoints to the `definitions/apic-api.yaml` file. 
    * Open the folder `common/models/` and see that Loopback created a `post.json` file with definitions for the Post model defined in the `apic-api.yaml` spec. you also see a `post.js` file with a function handling Post access requests. You see that the function has no implementations. You have to add methods corresponding to the `operationId` property in the YAML spec.  
    * Open the `server/model-config.json` file and see that Loopback added a property with Loopback configuration for the Post model,

        ```
        "Post": {
            "dataSource": null,
            "public": true
        }
        ```

    * The `dataSource` for `Post` is null. Datasources are defined in the `server/datasources.json` file. 

3. Add a Memory Connector for Post,
    See https://loopback.io/doc/en/lb3/Memory-connector.html

    * Define the built-in memory connector in `server/datasources.json`,

        ```
        {
          "db": {
            "name": "db",
            "connector": "memory"
          }
        }
        ```
    
    * Add the datasource for Post in `server/model-config.json`,

        ```
        "Post": {
            "dataSource": "db",
            "public": true
        }
        ```

4. Test your application,

    * Start the created application with `npm start` or `node .`,
    * Run `curl -X GET http://localhost:3000 -H 'Accept: application/json' -H 'Content-Type: application/json' ` 

        ```console
        $ curl -X GET http://localhost:3000 -H 'Accept: application/json' -H 'Content-Type: application/json' 
        {"started":"2019-07-14T14:14:07.068Z","uptime":474.229}
        ```

5. Clean up

    * shutdown the application with CTRL-c