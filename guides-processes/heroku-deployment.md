# Heroku Deployment

## Checklist

- **Dynamic Port Binding** : Heroku will give you a specific Port you must listen to. To allow Heroku to inject the port number, use ```const Port = process.env.PORT || 5000``` (Port 5000 can be any back-up port)

- **Specify Node Environment** : Need to tell Heroku the specific version of Node being used ```"engines": { "node": (version) }```

- ***Specify Start Script*** : Need to tell Heroku what commands to use to start the application

- **Create a .gitignore file** : put files to be ignored on upload in here (node_modules for sure)

## Steps

1. Install Heroku CLI and Create App
2. Login to Heroku in your terminal using ```heroku login```
3. ```heroku create``` : will give you webpage in the browser and git repo URL to push to(adding unique name after create will be the name for your url)
4. Check the remote ```git remote -v```. If not correct, make URL you are given in step 3 your remote ```git remote add heroku <insert URL here>``` (This should only happen if you deployed to a previous Heroku repo ex. You pushed to a previous Heroku repo, deleted it and created a new one)
5. Then push to that remote repo ```git push heroku main``` or ```git push heroku master```
6. ```heroku open``` will open the deployed application in your browser

## Tips
- Make sure your package.json is in the main directory
- Make sure the start script points to the right place

## Updating 
- When you need to update your application: Push changes to Github ```git push heroku main```
- This will rebuild the code, then use ```heroku open```

## Creating Postgres Database(Postgres Addon)
- Type ```heroku addons``` to check and see what addons you have for your app
- ```heroku addons:create heroku-postgresql:hobby-dev``` for the free postgres addon plan 
- This creates a database, and sets a ```DATABASE_URL``` environment variable (you can check by running ```heroku config```)
- To add a seed file for creating tables, use ```cat <file_name> | heroku pg:psql```
-*NOTE:* Unlike MySQL, when inserting values into a table you can't use double quotes for the values, Postgres considers them identifiers.
```INSERT INTO courses (id name) VALUES (1, 'Math')```
- Use ```heroku pg:psql``` to access Postgres CLI

# Connecting to Database
To Connect to the database you need to use the ENV variable DATABASE_URL
```javascript

const { Pool } = require('pg');
const pool = new Pool({
    connectionString: process.env.DATABASE_URL,
    ssl: {
        rejectUnauthorized: false
    }
});

module.exports = pool;

```

After database is connected, create your routes in the following manner:
```javascript

app.get('/api/students', async (req, res) => {
	try {
		const client = await pool.connect();
		const result = await client.query('SELECT * FROM student');
		res.send(result.rows);
		client.release();
	} catch (err) {
		console.error(err);
		res.send("Error " + err);
	}

});

```

# Logs
Here you can check error codes:
```heroku logs --tail``` : logs as streams of time-ordered events aggregated from the output streams of all your app and Heroku components, providing a single channel for all of the events.

[Getting Started Docs](https://devcenter.heroku.com/articles/getting-started-with-nodejs)
