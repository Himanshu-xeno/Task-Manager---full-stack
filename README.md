📝 Task Manager – Backend Setup (Day 1)

A simple full-stack Task Manager app. This README covers the Day 1 setup of the backend using Node.js, Express, MongoDB Atlas, and Mongoose, with full Git & GitHub integration.

---

DAY 1 : Project setup and Backend planning 

🚀 Goal : Set up a clean, secure, version-controlled backend for the Task Manager app using ⇒ 

- ✅ Express.js – backend server
- ✅ MongoDB Atlas – cloud database
- ✅ Mongoose – schema modeling
- ✅ dotenv – environment variable management
- ✅ Git & GitHub – version control & collaboration

Folder Structure : 

Task-manager/              # 👉 Root project folder
├── backend/              # 👉 Your backend server code
│   ├── server.js         # 👉 Entry point for Express server
│   ├── models/           # 👉 Mongoose schemas (e.g., Task.js)
│   ├── node_modules/     # 👉 Installed dependencies (ignored in Git)
│   ├── .env              # 👉 Secrets (never pushed)
│   ├── .gitignore        # 👉 Ignore node_modules & .env
│   ├── package.json      # 👉 npm config & scripts
├── [README.md](http://readme.md/)             # 👉 Project overview & setup instructions

---

## Step 1 : Project folder structure

- Creating a root project folder : Task-Manager.
- inside it add a backend/ folder.

---

## Step 2 : Initialize Node project

- firstly go inside /backend using ‘cd backend’ .
- run : npm init -y  ⇒ generate the package.json.
- Install the required packages/dependencies :

```bash
npm install express mongoose cors dotenv
npm install --save-dev nodemon
```

- Why to install them :

→ express = web server framework 

→ mongoose = Connects Node.js to MongoDB

→ cors  = Handles cross-origin requests (needed later for frontend)

→ dotenv = Loads the environment variables from .env securely 

→ nodemon = Auto-restarts the server when changes are made (dev only)

---

## Step 3 : Planned the Mongoose Schema

- Plan the Schema for the mongoDB
- save it in /backend/models/Task.js
- Model name here is Task

> We have a single collection : tasks
> 

Code for Task.js : 

```jsx
const mongoose = require('mongoose');

const taskSchema = new mongoose.Schema(
  {
    title :{
      type: String,
      required : true,
      trim : true,
    },
    completed :{
      type : Boolean,
      default : false,
    },
  },

  {timestamps : true}

);

module.exports = mongoose.model('Task', taskSchema);
```

---

## Step 4 : Setup server.js

- Created the /backend/server.js
- This is the backend entry point - it initializes the server and database connection.

→ `require('dotenv').config()` to load `.env`

→ `express()` app setup
→ `mongoose.connect()` to connect to MongoDB Atlas
→ A test route: `GET /` returns “Server is running 🚀”
→ `app.listen(PORT)` to start the server

Code for server.js : 

```jsx
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
require('dotenv').config();

// App setup
const app = express();
const PORT = process.env.PORT || 5000;

// Middleware
app.use(cors());
app.use(express.json());

// Test route
app.get('/', (req, res) => {
  res.send('Server is running 🚀');
});

// DB Connection
mongoose.connect(process.env.MONGO_URI)
  .then(() => console.log('✅ MongoDB connected'))
  .catch(err => console.error('❌ Connection error:', err));

// Start server
app.listen(PORT, () => {
  console.log(`Server listening on port ${PORT} 🔥`);
});

```

---

## Step 5 : MongoDB Atlas Setup

- Created a free MongoDB Atlas Cluster
- Created a Database User with `Read and write to any database`.
- Whitelisted your IP (`0.0.0.0/0` for dev).
- Copy your connection URI (mongodb+srv://...)

Reason to do this : Atlas is your cloud database. 

⇒ Your DB user lets your app connect securely — not your personal Atlas login.

---

## Step 6 : Create .env File

- Create the file `.env` inside the backend folder with the following:

```jsx
MONGO_URI=your_mongo_connection_string_here
PORT=5000
```

- Update  `.gitignore`.

```
node_modules/
.env
```

Reason to do so ⇒ 

Environment variables keep secrets out of your code.

`.env`must never be pushed to GitHub.

DO CHECK THIS PAGE : 

[.gitignore](https://www.notion.so/gitignore-222a056b8bf480e7a6abdf86181a0cd3?pvs=21)

---

## Step 7 : Test the server

- go back to : D:\Placements\Full Stack Development\Task-manager
- use the cd .. ⇒ to go backwards
- Run this now  :  npm run dev
- Confirmation news :

[nodemon] starting `node server.js`
[dotenv@17.0.0] injecting env (2) from .env – 🔐 encrypt with dotenvx: [https://dotenvx.com](https://dotenvx.com/)
Server listening on port 5000 🔥
✅ MongoDB connected

---

## Step 8 : Git and GitHub setup

1. Initialize Git:
    
    git init
    
2. Add a .gitignore file with:
    
    node_modules/
    
    .env
    
3. Create a GitHub repo and connect:
    
    git remote add origin https://github.com/your-username/task-manager-backend.git
    
    git branch -M main
    
    git add .
    
    git commit -m "Initial commit: backend setup"
    
    git push -u origin main
    
    ---
    

## 🔗 Helpful Links

- Express.js: https://expressjs.com/
- Mongoose: https://mongoosejs.com/
- MongoDB Atlas: https://www.mongodb.com/cloud/atlas
- dotenv: https://github.com/motdotla/dotenv
- GitHub Docs: https://docs.github.com/en/get-started

---

## ✅ Summary of Day 1

- Clean folder structure
- Express.js server created
- MongoDB Atlas cluster connected
- Mongoose model created
- Environment variables set in .env
- Project pushed to GitHub

Next Up: Routes, Controllers, and CRUD operations for Tasks.