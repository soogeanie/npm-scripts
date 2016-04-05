# How to: Dev Environment with Node.JS and NPM


I'm using Node.JS and npm scripts to automate a few handy dandy things like compiling my scss, compressing EVERYTHING, and running my local server.


Don't worry if you're not a terminal expert (I'm not one either!). Sometimes online resources are filled with technical jargon and it can get confusing for someone new. Hopefully, I can explain this in a human-centric way so that you can follow along and have a awesome dev environment too!


****
### Step by Step Guide
1. Create your project folder. I like to store all my project folders in a folder named Sites that lives in my Home(:house:) folder.

2. Open your project folder in your text editor of choice. Mine is [Atom](https://atom.io).

3. Go to your project folder in your terminal.
  * If you type `ls` in your terminal, it will tell you what folders are available wherever you are currently.

  * type `cd foldername` to get into the folder. CATCH: You have to `cd foldername` into the folder that your folder is in. Inception... -- cd means change directory

    * Example: Project Juice Folder is inside Projects folder which is inside Sites folder which is inside the Home Folder.

    * When you open your terminal, you'll be in your home folder. Type `ls` to double check. You should see your Sites folder.

    * Then, you will type `cd Sites` to go into your Sites folder.

    * And then, you will type `cd Projects` to go into your Projects folder.

    * And lastly, you will type `cd Project Juice` to go into your Project Juice folder.

    * At any time if you don't know where you are type `pwd` and the terminal will tell you your file path thing.

    * I don't know why this took me so many google searches to find...but if you want to go UP a folder -- type `cd ..` into your terminal.

    * If you get lost, type `cd` and you'll end up in your home directory.

4. Once you're in your folder, then type `touch .nvmrc` - touch means create a file, so we're creating a file named .nvmrc - this is where we will put our version of node.

5. Go to your text editor and open the .nvmrc file. Check on [Node.JS](https://nodejs.org) to see what the most up to date version is and type that in.

  * If it says `v4.4.2 LTS`, then all you need to do is type `4.4.2` into your .nvmrc file.

6. Go back to your terminal, make sure you're in the proper folder (Project Juice for this example), and type `nvm install` -- this will install the version of node that we just put in the .nvmrc file.

7. After node finishes installing, make sure you're still in the proper folder, and type `nvm use` -- this will use the version of node that we just put in the .nvmrc file.

  * You only have to type `nvm use` once per project. If you create a new project, make sure you type `nvm use` before running your dev script.

8. After node finishes installing, type `npm init`. This is the process that will create your packages.json file. -- If you don't want to go through this process yourself, just copy my packages.json file and change the project name, author, and description.

9. Here's one of the most important parts: double check the folders in your scripts. Mine are set to compile my stylesheets/scripts/images from src to dist.

10. If you don't want to use http-server, follow the alternative path below for using Express.JS along with EJS or Jade.

11. Made all your adjustments, additions, and subtractions? Let's run the install script! Go to your terminal (you should still be in your Project Juice folder) and type `npm install` -- this will install all your dependencies and devDependencies.

  * This setup includes lint. If you don't want to lint your code, then remove it from the scripts and the devDependencies.

  * If you DO want to include lint, then type `./node_modules/eslint/bin/eslint.js --init` into your terminal and go with `answer questions about your style`

  * Here's mine: ![My Lint Preferences](/dist/images/lint-qa.png)

12. Installation a success? Type `npm run dev` to start up your environment!

****
* Want to use Express.JS with EJS or Jade?
  1. Create a Views folder (on the same level as your dist and src folder) that contains your index.ejs or index.jade file.

  2. Add this above your devDependencies in your packages.json file.
  ```javascript  
  "dependencies": {
      "express": "4.13.4",
      "ejs": "2.4.1"
    },
  ```

  3. Edit your `"start"` script from `node ./node_modules/http-server/bin/http-server ./dist` to `node server.js`

  4. Create the server.js file or rename your index.js file.

    * If you followed the steps of `npm init`, then it would have created a index.js as your entry point (unless you changed this to something else). You will need to rename this file to server.js.

    * If you just copied the packages.json file, then you will need to create a server.js file. This will be in the same level as your dist folder, packages.json file, and your .nvmrc file.

  5. This will go into your server.js file
  ```javascript
  var express = require("express");

  var app = express();

  app.use(express.static("public"));
  app.set("view engine", "ejs");

  app.get("/", function(req, res) {
    res.render("index");
  });

  app.listen(3000);
  ```

  6. If you want to use Jade instead of EJS? Just make sure you make change ejs to jade in the server.js file
  ```javascript
  app.set("view engine", "ejs");
  ```
  to
  ```javascript
  app.set("view engine", "jade");
  ```

  7. Don't forget to run npm install to install Express and EJS before running your dev script.

***

**A few notes:**
* If your server is already running, type `ctrl-c` into your terminal window where your server is running to stop the server. The same applies to any npm scripts you may run in the future.

* You have to type npm run imagemin whenever you want to compress images because I haven't figured out how to do this onchange... I'll update it once I've figured it out.

* Don't forget to create all your folders and files. Type `mkdir foldername` into the terminal to create a folder and `touch filename` to create the file. You can always take a look at the folder structure of this project if you need a more concrete example.

* Include `node_modules` in your `.gitignore` file so it doesn't get uploaded to your repo.

* Thank you to this awesome article about [npm scripts](https://css-tricks.com/why-npm-scripts/)! I've learned a lot and hopefully you have too!

***
I would love any and all feedback (good or bad), especially if you have any comments on how I can make this even easier to follow and use. Thanks!
