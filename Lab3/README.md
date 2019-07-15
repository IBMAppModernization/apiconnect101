# Lab3 - Publish your API

## API Connect
API Connect is the API Management framework built by IBM. API Connect integrates with Loopback and is available as an API Connect service on IBM Cloud.

See: https://developer.ibm.com/apiconnect/getting-started

# Lab3

1. Create API Connect service instance on IBM Cloud
    * Login to https://cloud.ibm.com,
    * Go to the Catalog
    * Search the catalog... for `API Connect` in the `Integration` category,
    * Click the `API Connect` service panel,
    * Optionally, edit the service name, location, and space,
    * Click the `Create` button,

    * If the page does not load correctly in Google Chrome, try Firefox,

    * By default, API Connect creates a Sandbox Catalog,
    * Open the Sandbox Catalog,
    * Currently, there are no products published in the Sandbox,


2. From the local API Designer publish the product as `stage only` to the IBM Cloud

    * Start the API Designer on your localhost to load the products created in Lab1 and Lab2,

    ```console
    $ apic edit
    ```

    * Go to the APIs tab,
    * Select the `apic-api 1.2.0` API,
    * Go to the `Info` section, and change the `Version` to `1.2.1`,
    * Go to the `Schemes` section,
    * The API Connect service on IBM Cloud requires and allows only the `https` Scheme, so disable the `http` protocol and enable only the `https` protocol,
    * Click the `Validate` icon,
    * Click the `Save` icon,
    * From the dropdown in the top right, select the `Add to existing products`,
    * Select the `1.2.0` option,
    * Click the `Add` button,


    * Go to the Products tab,
    * Open the `apic-api 1.2.0` product,
    * In the Plan designer, go to the `Default Plan` section, and in the `1 API included` section, unfold the `apic-api 1.2.0` to list all the API methods,
    * Uncheck the writeable API methods:
        * Post.create
        * Post.updateAll
        * Post.updateById
        * Popst.deleteById
    * Click the `Save` button,
    
    * Click the Publish button,
    * Select `Add and Manage Targets`,
    * Select the `Add IBM Cloud target` option,
    * Configure the settings corresponding to those in your API Connect service instance:
        * Select the Region,
        * Select the Organization and Space,
        * API Connect loads the catalogs that match the configured settings, if correct you should see the catalog named `Sandbox`, 
        * Select `Sandbox` catalog and click `Next`,
        * Leave the application name empty for now, and select `None`,
        * Click the `Save` button,
        * You have now added a target for the product,

        * Again click the Publish button,
        * Select the `Sandbox (sb)` target, 
        * Check the `Stage Only` option,
        * Click the `Publish` button,

    * Go back to https://cloud.ibm.com,
    * In the `Resource summary` select the `View resources` link,
    * Under `Cloud Foundry Services`, select the API Connect instance you created,
    * Select the `Sandbox` catalog,
    * Under the `Products` tab you should see the product that you ppublished in the previous step, the `State` should display `Staged`,

3. Add a Developer Portal,

    * In the Sandbox catalog, click the Settings,
    * Go to the `Portal` in the left column,
    * In the `Portal Configuration`, under `Select portal` dropdown, select the `IBM Developer Portal`,
    * Click the `SSave` icon,
    * You will see a popup window `Creating the developer portal...  Creating the developer portal for catalog 'Sandbox' may take a few minutes. You will receive an email when the portal is available."
    * Click `OK`,

4. Publish the staged product,

    * Go back to the `Products` tab,
    * Select the options dropdown to the right of the `apic-api 1.2.0` staged product,
    * Click `Publish`
    * Click `Publish`
    * The state of the product should change to `Published`
    
5. Sign up, Add an Application and Subscribe to the APIs

    * Keep at eye at your email inbox and wait for the email with subject `Your new site https://sb-<your-name>.developer.us.apiconnect.ibmcloud.com has been created.` email,
    * Open the email and click on the `change the password for the admin user` link, click the `Log in` link, change your password, and click `Save`,

    * Logout of the `admin` account,
    * Click the `Create an account` link,
    * Sign up with your personal information,
    * Click the `Create an account` button,
    * You should receive a `Thank you for signing up for our APIs` email with an activation link,
    * After successful activation, login with your confirmed developer account,
    * Click the `Apps` tab, and click the `Create new App` button,
    * For `Title` add `APIC App`, and click `Submit`,
        * Save the Client Secret and Client ID,
        * E.g. Client ID: tI2vE6mL7qX1lX1qV7uU0kX1bA5mA2iQ5bN6wP4pX6iL6gA0qL
        * Client Secret: 2bfa445e-5d83-4c22-9a9d-e851f87a080f
    * Go to the `API Products` tab,
    * Select the `apic-api (1.2.0)(1 API included)` API Product,
    * Under Plans, select the `apic-api 1.2.1` plan and click the `Subscribe` button,
    * In the `Subscribe` window, select the `APIC App` option,
    * Click the `Subscribe` button,
    * At the top of the page, you should see a `Successfully subscribed to this plan` notification,
    * Go to `Apps`, `APIC App` application, and in the `Subscriptions` window you should see your subscription listed now,

    * Go to the `Getting Started` tab,
    * Click the `Explore our APIs` button,
    * Or go directly to the `API Products` page,
    * Select the `apic-api (1.2.0)(1 API included)` API Product,
    * In the left menu, under APIs, select the `apic-api` option,
    * The Explorer window opens,

    * Remember that we did not select an Application when we staged and published the API, so currently you will get a 500 error when you test out the API endpoints.

        ```console
        curl GET 'https://api.us-south.apiconnect.appdomain.cloud/remkohdevusibmcom-dev/sb/api/Posts'
        curl: (6) Could not resolve host: GET
        { "httpCode":"500", "httpMessage":"Internal Server Error", "moreInformation":"Backside URL invalid" }
        ```







    
    
    

