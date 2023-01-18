![d5hqar2idkoefh6fjtpu](https://user-images.githubusercontent.com/96712943/213082489-0fdd88f8-60c4-499f-8339-a9952716f9fa.png)
# REACT Deployment

## Deploying 

- ```npm run build``` creates a ```build``` directory with a production build of your app. Set up your favorite HTTP server so that a visitor to your site is served ```index.html```, and requests to static paths like ```/static/js/main```. ```<hash>.js``` are serverd with the contents of the ```/static/js/main```. ```<hash>.js``` file. For more information see the [production build](https://create-react-app.dev/docs/production-build) section.

## Static Server

- For environments using [Node](https://nodejs.org/), the easiest way to handle this would be to install [serve](https://github.com/vercel/serve) and let it handle the rest:
```
npm install -g serve
serve -s build
```
- The last command shown above will serve your static site on the port **3000**. Like many of [serve](https://github.com/vercel/serve)'s internal settings, the port can be adjusted using the ```-l``` or ```--listen``` flags:
```
serve -s build -l 4000
```

- Run this command to get a full list of options available:
```
serve -h
```

## Other Solutions

- You don’t necessarily need a static server in order to run a Create React App project in production. It also works well when integrated into an existing server side app.
- Here's a programmatic example using [Node](https://nodejs.org/) and [Express](https://expressjs.com/):
```javascript
const express = require('express');
const path = require('path');
const app = express();

app.use(express.static(path.join(__dirname, 'build')));

app.get('/', function (req, res) {
  res.sendFile(path.join(__dirname, 'build', 'index.html'));
});

app.listen(9000);
```
- The choice of your server software isn’t important either. Since Create React App is completely platform-agnostic, there’s no need to explicitly use Node.
- The ```build``` folder with static assets is the only output produced by Create React App.
- However this is not quite enough if you use client-side routing. Read the next section if you want to support URLs like ```/todos/42``` in your single-page app.

## Serving Apps and Client-Side Routing

- If you use routers that use the HTML5 ```pushState``` [history API](https://developer.mozilla.org/en-US/docs/Web/API/History_API#Adding_and_modifying_history_entries) under the hood (for example, [React Router](https://github.com/ReactTraining/react-router) with ```browserHistory```), many static file servers will fail. For example, if you used React Router with a route for ```/todos/42```, the development server will respond to ```localhost:3000/todos/42``` properly, but an Express serving a production build as above will not.
- This is because when there is a fresh page load for a ```/todos/42```, the server looks for the file ```build/todos/42``` and does not find it. The server needs to be configured to respond to a request to ```/todos/42``` by serving ```index.html```. For example, we can amend our Express example above to serve ```index.html``` for any unknown paths:
```javascript
app.use(express.static(path.join(__dirname, 'build')));

-app.get('/', function (req, res) {
+app.get('/*', function (req, res) {
   res.sendFile(path.join(__dirname, 'build', 'index.html'));
 });
``` 
- If you’re using [Apache HTTP Server](https://httpd.apache.org/), you need to create a ```.htaccess``` file in the ```public``` folder that looks like this: 
```javascript
Options -MultiViews
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^ index.html [QSA,L]
```
- It will get copied to the ```build``` folder when you run ```npm run build```.
- If you're using [Apache Tomcat](https://tomcat.apache.org/), you need to follow this [Stack Overflow answer](https://stackoverflow.com/a/41249464/4878474).
- Now requests to ```/todos/42``` will be handled correctly both in development and in production.
- On a production build, and when you've [opted-in](https://create-react-app.dev/docs/making-a-progressive-web-app#why-opt-in), a [service worker](https://developers.google.com/web/fundamentals/primers/service-workers/) will automatically handle all navigation requests, like for ```/todos/42```, by serving the cached copy of your ```index.html```. This service worker navigation routing can be configured or disabled by [ejecting](https://create-react-app.dev/docs/available-scripts#npm-run-eject) and then modifying the ```navigateFallback``` and ```navigateFallbackWhitelist``` options of the ```SWPrecachePlugin``` configuration.
- When users install your app to the homescreen of their device the default configuration will make a shortcut to ```/index.html```. This may not work for client-side routers which expect the app to be served from ```/```. Edit the web app manifest at ```public/manifest.json``` and change ```start_url``` to match the required URL scheme, for example: 
```javascript
"homepage": "http://mywebsite.com/relativepath",
```
- This will let Create React App correctly infer the root path to use in the generated HTML file.
  - **Note**: If you are using ```react-router@^4```, you can root ```<Link>```s using the ```basename``` prop on any ```<Router>```.
  - More information [here](https://reacttraining.com/react-router/web/api/BrowserRouter/basename-string).
- For Example:
```javascript
<BrowserRouter basename="/calendar"/>
<Link to="/today"/> // renders <a href="/calendar/today">
```
- Serving the Same Build from Different Paths
  - Note: this feature is available with ```react-scripts@0.9.0``` and higher.
- If you are not using the HTML5 ```pushstate``` history API or not using client-side routing at all, it is unnecessary to specify the URL from which you app will be served. Instead, you can put this in your ```package.json```:
```javascript
"homepage":".",
```
- This will make sure that all the asset paths are relative to ```index.html```. You will then be able to move your app from ```http://mywebsite.com``` to ```http://mywebsite.com/relativepath``` or even ```http://mywebsite.com/relative/path``` without having to rebuild it.

## Customizing Environments Variables for Arbitrary Build Environments

- You can create an arbitrary build environment by creating a custom ```.env``` file and loading it using [env-cmd](https://www.npmjs.com/package/env-cmd).
- For example, to create a build environment for a staging environment:
  1. Create a file called ```.env.staging```
  2. Set environment variables as you would any other ```.env``` file (e.g. ```REACT_APP_API_URL=http://api-staging.example.com```)
  3. Install [env-cmd](https://www.npmjs.com/package/env-cmd)
```javascript
npm install env-cmd --save
# or 
yarn add env-cmd
```
  4. Add a new script to your ```package.json```, building with your new environment:
```javascript
{
  "scripts": {
    "build:staging": "env-cmd -f .env.staging npm run build"
  }
}
``` 
- Now you can run ```npm run build:staging``` to build with the staging environment config. You can specify other environments in the same way.
- Variables in ```.env.production``` will be used as fallback because ```NODE_ENV``` will always be set to ```production``` for a build.

## [AWS Amplify](https://console.amplify.aws/)

- The AWS Amplify Console provides continuous deployment and hosting for modern web apps (single page apps and static site generators) with serverless backends. The Amplify Console offers globally available CDNs, custom domain setup, feature branch deployments, and password protection.
  1. Login to the Amplify Console [here](https://console.aws.amazon.com/amplify/home).
  2. Connect your Create React App repo and pick a branch. If you're looking for a Create React App + Amplify starter, try the [create-react-app-auth-amplify starter](https://github.com/swaminator/create-react-app-auth-amplify) that demonstrates setting up auth in 10 minutes with Create React App.
  3. The Amplify Console automatically detects the build settings. Choose *Next*.
  4. Choose *Save and Deploy*.
- If the build succeeds, the app is deployed and hosted on a global CDN with an [amplifyapp.com](http://amplifyapp.com/) domain. You can now continuously deploy changes to your frontend or backend. Continuous deployment allows developers to deploy updates to their frontend and backend on every code commit to their Git repository.

## [Azure](https://azure.microsoft.com/)

- Azure Static Web Apps creates an automated build and deploy pipeline for your React app powered by GitHub Actions. Applications are geo-distributed by default with multiple points of presence. PR's are built automatically for staging environment previews.

[Getting Started Docs](https://create-react-app.dev/docs/deployment/)
