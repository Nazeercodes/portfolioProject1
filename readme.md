<!-- Here we will maintain the note of making the full stack project from start to finish -->
# Full stack project guide

## setting up the project
- install node.js
- making two folders one for backend another one for frontend
- npm intit in the backend folder
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
