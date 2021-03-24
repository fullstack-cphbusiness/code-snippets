# Code-snippets used in fullstack JavaScipt/Typescript

## How to user the logger.ts middleware
### First install these packages/type-definitions:
```
npm install winston morgan
npm install @types/morgan --save-dev
```
### In the root of your project create a logs folder as described below
Create a folder (in the root of the project) called logs
Add an file to the folder called **```.keep```**  with the content *necessary since git does not commit/push empty folders*

Add this to your .gitignore
```
# ignore all logs files
logs/*
# don't ignore keep files
!.keep
```
# In your ```app.ts``` file add this (figure out where)
```
import logger, { stream } from "./middleware/logger";
const morganFormat = process.env.NODE_ENV == "production" ? "combined" : "dev"
app.use(require("morgan")(morganFormat, { stream }));
app.set("logger", logger) //This line sets the logger with a global key on the application object
//You can now use it from all your middlewares like this req.app.get("logger").log("info","Message")
//Level can be one of the following: error, warn, info, http, verbose, debug, silly
//Level = "error" will go to the error file in production
logger.log("info", "Server started"); //Example of how to use the logger
```

## Get the logger.ts file
Create a file logger.ts in the middleware folder and copy/paste the content of logger.ts into this file

# Using the logger-middleware
- Run your project and observe how all (depending on where you added the middleware) requests are logged to the terminal
- Observe that NOTHING is writen to the logfiles
- Now CLOSE the server (nodemon are not watching your .env file) and add this to your **.env** file:

  ```NODE_ENV=production```
- Restart the server ```npm run dev``` and observe how things are NOT logged to your terminal but to the log-files
