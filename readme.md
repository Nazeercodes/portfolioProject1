<!-- Here we will maintain the note of making the full stack project from start to finish -->
# Full stack project guide

## setting up the project
- install node.js
- making two folders one for backend another one for frontend
- npm init in the backend folder
### making a git repository
- make a git repository in github then follow the below steps in the terminal of backend
- git init
- git add .
- git commit -m "message"
- git branch -M main
- git remote add origin (the repository link)
- git push -u origin main
- keep pushing the changes
### adding other files in backend folder
- adding .env file
- adding .gitignore file and adding the files not necessary 
to be push in git(search gitignore generator and search node
copy and paste)
- adding the public folder and adding temp file to it
- adding src folder
- easiest way to add files is using command line
- going to src directory using cd src and adding files using touch
- touch constant.js app.js index.js

### adding files in package.json
- adding "type":"module" so that we can use import syntax
- adding nodemon to restart server every time we change something
in index.js
- npm i -D nodemon 
- to use nodemon for index.js so that every time it gets restart
we will make a script
"dev": "nodemon src/index.js" in place of test script

### adding files and folders in src folder
- mkdir controllers db utils models routes middlewares

### adding prettier
this will help to maintain consistent code writing if working in a 
team, like using the same spacing, commas etc by different team members
- npm i -D prettier
- adding .prettierrc in src folder
    {
    "singleQuote": false,
    "bracketSpacing": true,
    "tabWidth": 2,
    "trailingComma": "es5",
    "semi": true
    }
- adding .prettierignore in src folder
    /.vscode
    /node_modules
    /.dist
    *.env
    .env
    .env.*
## connecting to the db
- go to mongodb and create a project
- we usually use the tabs of network access and db access to change anything
- in production level we never allow the ip address to be allowed from everywhere
- but for this project we will allow from everywhere by putting 0.0.0.0/0 from network access
- adding an user from db access and giving access to read and write (xe0sFbemeTluNJO0)
- go to database tab connect and copy the string url 
- connecting through compass
- adding the MONGODB_URI to the env variable also give a port
- remove the last slash from the uri
- go to constants in src to give a name of db so that we can connect(we are putting 
in the constants file because every time we change something it will change in entire db)
- export const DB_NAME= "backendapp"
- we can have two approach to connect the db, either making a db folder separately and then 
importing it into the index.js file or directly writing in the index.js file
- installing three packages npm i mongoose dotenv express
- after installing always check the package.json file if they are installed or not
### connecting to the db through index.js file

import mongoose from "mongoose"
import {DB_NAME} from "./constants";
import express from "express"
const app =express()
(async()=>{
    try{
        await mongoose.connect(`${process.env.MONGO_URI}/${DB_NAME}`)
        app.on("error",(error)=>{
            console.log("Error", error);
            })
    }
    app.listen(process.env.PORT,()=>{
        console.log(`App is listening on port${process.env.PORT}`);
    })
    catch(error){
        console.log("Error: ", error);
        throw err;
    }
})()

### connecting to the db through the db folder(we will use this method)
- make an index.js file in db directory
import mongoose from "mongoose";
import {DB_NAME} from "../constants.js";

const connectDB= async()=>{
    try{
        const connectionInstance= await mongoose.connect
        (`${process.env.MONGODB_URI}/${DB_NAME}`)
        console.log(`\n MongoDb connected!! DB host:${connectionInstance.connection.host}`);
    }
    catch{
        console.log("MongoDb connection error", error);
        process.exit(1)
    }
}

export default connectDB
- import connectDB in src index.js file
import dotenv from "dotenv"
import connectDB from "./db.index.js";
dotenv.config({
    path:'./env'
})
connectDB()

- to use the import syntax for dotenv we will use some experimental features
in package.json file so that code have the consistency, but this syntax will come in future
- in package.json file, in the script ->
"dev" : "nodemon -r dotenv/config --experimental-json-modules src/index.js"
done!
-make sure while writing the password in the env file you remove the two arrow brackets from uri
