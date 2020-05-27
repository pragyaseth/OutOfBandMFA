# Out Of Band MFA

> Web app to prompt out of box MFA for user validation

## Pre-requisites
> NPM (install npm from here: https://www.npmjs.com/get-npm)
> CA certified certifcate or opensSSL to generate self-signed cert

## Create a single page OIDC app in Okta

> 1. Go to Admin console, Applications tab and Choose 'Add Applications' button.
> 2. Select 'Create New App' option. Platform should be set to 'Single Page App (SPA)'.
> 3. Set the application name as 'MFA for Identity Verification'
> 4. Set the login redirect uri to be the web app's URI (e.g. https://hostname:port/implicit/callback where hostname can be localhost and port can be 8080)
> 5. Set the initiate login uri as https://hostname:port (e.g. https://localhost:8080)
> 6. Save the settings and assign the app to all users who need access to 'MFA to Identity Verification' app.

## Server App Setup
Download the zip file and unzip under desired location. Go to the folder '
MGM-OutOfBandMFA'  
Go to the file src/server.js and update the following values

> const orgURL = 'https://yourdomain.oktapreview.com'  
> const sswsToken = 'dbsdfbsbsfnfnfnnnndgbnfndbsdfbsbsfnfnfnnnndgbnfn' (This should an admin API token)  
> const client = 'dbdbbbbb' (client ID of the 'MFA for Identity Verification' app created in Okta)  
> const host = 'https://localhost' (hostname for server app)  
> const port = '3000' (port for server app)
> .
> .
> .
> var options = {
> key: fs.readFileSync('C:\\OutOfBandMFA-master\\OutOfBandMFA-master\\src\\cert.key'), (path to the private key)
>  cert: fs.readFileSync('C:\\OutOfBandMFA-master\\OutOfBandMFA-master\\src\\cert.pem') (path to the sertificate)
> };

Save changes

Go to the file src/api.js and update the base URL

> baseURL: 'https://localhost:3000/'

Save changes

Install server dependencies from terminal

> npm install express cors @okta/jwt-verifier axios simple-node-logger

Start the server

> node ./src/server

## web-app setup
Go to the file src/router/index.js and update the following values

> const client = 'dbdbbbbb'  
> const orgURL = 'https://yourdomain.oktapreview.com'  
> const baseRedirect = 'https://localhost:8080'  

Save changes

Go to the file build/dev-server.js and update the following host value

> const uri = 'https://localhost:' + port
> .
> .
> .
> const server = https.createServer({
>  key: fs.readFileSync('C:\\OutOfBandMFA-master\\OutOfBandMFA-master\\src\\cert.key'), (path to the private key)
>  cert: fs.readFileSync('C:\\OutOfBandMFA-master\\OutOfBandMFA-master\\src\\cert.pem') (path to the sertificate)
> }, app).listen(port)

Save changes

Go to the file config/index.js and update the port value. Save changes.

From another terminal window, install vue-cli, bootstrap and Okta SDK

> npm install bootstrap-vue bootstrap @okta/okta-vue vue-cli

Go to the file src/components/DisplayUser.vue and update image src path to point to the server location for the logo.

Go to the file src/components/Home.vue and update image src path to point to the server location for the logo.

Start server

> npm run dev
# MGM-OutOfBandMFA
