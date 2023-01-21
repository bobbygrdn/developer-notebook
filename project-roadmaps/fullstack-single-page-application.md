# Full-Stack Single Page Application

## Checklist
- **Entity Relational Diagram**
- **Client-Server_database-Diagram**
- **Create a Database**
- **ExpressJS Server** connected to the database
- **FrontendJS** that talks to the Server through an AJAX call **These are miminum requirements**

## Steps

1. **Create two diagrams:**
    1. ERD
        1. 2 x Tables with a One-To-many Relationship
    2. Client - Server - Database
        1. How do you draw a picture to show how these systems are connected?
        2. What information travels between each system?
        3. How do they talk to each other?
        4. What does each system do?
2. **Create Database**
    1. 2 x Tables with a One-To-Many Relationship
    2. Add at least 15 records
3. **Create Server**
    1. Install PG
    2. Connect to DB
    3. Setup Middlewares
        1. Bodyparser
        2. Cors
        3. Morgan
    4. Create CRUD Routes
        
        **important**: Make all your routes begin with the url path /api/. eg. `app.get(’/api/cats’,…)`
        
    5. Queries the DB then sends appropriate data
4. **Frontend**
    1. Add this like to your “server.js” file, above all of your routes: `app.use(express.static(’public’))` (this line ensures that anyone visiting the “root path” of your server, “localhost:3000/”, will receive an “index.html” page, and not go in to a route)
    2. Create “publicindex.html” page
    3. Create “public/app.js” page
    4. Connect app.js to index.html
    5. In app.js, make an AJAX call to your server route and display some data
    6. BONUS: 
        1. Add frontend features that make AJAX requests to different server routes