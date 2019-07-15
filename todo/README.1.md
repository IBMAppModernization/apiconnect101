# Labx - generate model from swagger

* Download the custom Swagger spec to the definitions folder,
    ```
    $ cd apic-szirine-api
    $ wget https://raw.githubusercontent.com/remkohdev/szirine-api/master/api/szirine-api-simple-swagger.yaml -O definitions/szirine-api-swagger-v2.yaml
    ```

* Create the model from the downloaded Swagger spec for both `swagger_api` and `Post`,
    ```
    $ apic loopback:swagger -f definitions/szirine-api-swagger-v2.yaml --skip-cache
    ? Enter the swagger spec url or file path: szirine-swagger-v2.yaml
    Loading szirine-swagger-v2.yaml...
    ? Select models to be generated: (Press <space> to select, <a> to toggle all, <i> to inverse selection)
    o swagger_api, 
    x Post
    ? Select the data-source to attach models to: (no data-source)
    Creating model definition for swagger_api...
    Creating model definition for Post...
    Model definition created/updated for swagger_api.
    Model definition created/updated for Post.
    Creating model config for swagger_api...
    Creating model config for Post...
    Model config created for swagger_api.
    Model config created for Post.
    Generating /apic-szirine-api/server/models/swagger-api.js
    Models are successfully generated from swagger spec.
    Done running LoopBack generator

    Updating swagger and product definitions
    Created /apic-szirine-api/definitions/apic-szirine-api.yaml swagger description
    ```

