# RESTful Express Server

## Starting Your Server Build

In any Express Server you will need to start by following some simple steps to get your project started. Performing these steps can be in any order, but the below order is what we recommend.
1. Initializing the Node Package Manager(NPM)
   1. ```npm init -y``` 
   This piece of code initializes the *Node Package Manager* and creates your *package.json* file. Your *package.json* file is your blueprint for your server and it holds all of your dependancies, scripts and other information ragarding your server.
2. Installing Packages
   1. ```npm install express```
   This piece of code installs *Express* to be used in your project. 

    Using this terminal command you will create your *node_modules* folder and your *package-lock.json*.

    The *node_modules* folder holds every piece of information about your dependencies you have installed so you may use the package in your project.
    **THIS FOLDER SHOULD NOT BE MODIFIED OR TOUCHED**
    The *package-lock.json* file is the blue print to your project and automatically generates for any operation where your NPM modifies either your *node_modules* tree or the *package.json* file. This file is used to keep track of the exact version of every package installed so that it may be exactly replicated for each user even if packages are updated by the maintainers.
    **THIS FILE SHOULD NOT BE MODIFIED OR TOUCHED**
   2. ```npm install node```
   This piece of code installs *Node* to be used in your project.
   Using this terminal command you will install node as a dependancy into your project so you can use it to run your server when it is in a development or deployment status.
   ```javascript
   // Starting your server using node will be done using the below code snippet
    node server.js
   ```
   3. ```npm install nodemon```
   This piece of code installs *Nodemon* to be used in your project.
   Using this terminal command you will install *Node* as a dependancy into your project so you can use it to run your server when it is in a development status. This is a useful package because it will allow you to keep your server running and implement changes when you save your file without the need for restarting your server.
   ```javascript
   // Starting your server using node will be done using the below code snippet
    nodemon server.js
   ```
   4. ```npm install pg```
   This piece of code installs Pg to be used in your project.

    Using this terminal command you will install *PG* as a dependancy into your project so you can connect to a database from your server and to override the environment variables used by PostgreSQL.

## Code Snippets

In any Express Server you will need several bits of code to run the basic functionality of the server.
There are three parts to set up a basic Express Server:
1. Setting Up Dependencies:
```javascript
const express = require('express');
const app = express();
```
2. Handling Requests with Routes:
```javascript
// Basic 'GET' route to get all the data in a given table
app.get('[URL PATH]', async (req,res) => {
	try {
		const data = await pool.query('SELECT * FROM [TABLE NAME];');
		res.send(data.rows);
	} catch (err) {
			console.error(err.message);
	};
});

// Basic 'GET' route to get all the data in a given table at the given id
app.get('[URL PATH]:id', async (req,res) => {
	let id = req.params.id;
	try {
		const data = await pool.query('SELECT * FROM [TABLE NAME];');
		res.send(data.rows[id]);
	} catch (err) {
			console.error(err.message);
	};
});

// Basic 'POST' route to input data into a given table
app.post('[URL PATH]', async (req,res) => {
	let obj = req.body;
	try {
			const data = await pool.query(`INSERT INTO [TABLE NAME] ([COLUMN1], [COLUMN2], [COLUMN3]) VALUES ('${obj.[COLUMN1]}', '${obj.[COLUMN2]}', '${obj.[COLUMN3]}');`);
			res.send('[MESSAGE SENT TO THE USER]');
		} catch (err) {
				console.error(err.message);
		};
});

// Basic 'PATCH' route to modify data into a given table at the given id
app.patch('[URL PATH]:id', async (req,res) => {
	let id = req.params.id;
	let obj = req.body;

	if(obj.[COLUMN]) {
		try {
			const data = await pool.query(`UPDATE [TABLE] SET [COLUMN NAME] = '${obj.[COLUMN NAME]}' WHERE id = '${id}';`);
			res.send('[MESSAGE SENT TO THE USER]');
		} catch (err) {
				console.error(err.message);
		};
	} else if(obj.[COLUMN]) {
		try {
			const data = await pool.query(`UPDATE [TABLE] SET [COLUMN NAME] = '${obj.[COLUMN NAME]}' WHERE id = '${id}';`);
			res.send('[MESSAGE SENT TO THE USER]');
		} catch (err) {
				console.error(err.message);
		};
	} else if(obj.[COLUMN]) {
		try {
			const data = await pool.query(`UPDATE [TABLE] SET [COLUMN NAME] = '${obj.[COLUMN NAME]}' WHERE id = '${id}';`);
			res.send('[MESSAGE SENT TO THE USER]');
		} catch (err) {
				console.error(err.message);
		};
	} else {
		console.error(err.message);
	};
});

// Basic 'DELETE' route to delete data in a given table at the given id
app.delete('[URL PATH]:id', async (req,res) => {
	let id = req.params.id;

	try {
			const data = await pool.query(`DELETE FROM pets WHERE id = '${id}'`);
			res.send('[MESSAGE SENT TO THE USER]');
		} catch (err) {
				console.error(err.message);
		};
});
```
3. Listen on a Port:
```javascript
app.listen([PORT NUMBER OR PORT VARIABLE], () => {
	console.log('Server is running on [PORT NUMBER OR PORT VARIABLE]');
});
```