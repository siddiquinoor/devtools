## Getting Started with React with Node JS

#

### Setup and Running
1. First we need to install Node.js. Head over to 'https://nodejs.org/en/download/' then download and install the version of Node.js depending on your operating system.

2. Create a folder for the new project and install React into that folder

        $~ mdkir NodeJS
        $ cd NodeJS
        $ NodeJS mkdir blog
        $ NodeJS cd blog
        $ blog npx create-react-app client

3. Now create another folder inside `blog` and create package.json file for NodeJS

        $ blog mkdir posts
        $ blog cd posts
        $ posts npm init -y

    This will create a package.json file, the boiler plate of our NodeJS applicaiton

    Now that our Node project is ready to add dependency.

4. We will use couple of **Node packages**, let's add them in our project 

        $ posts npm install express cors axios nodemon

5. Let's go back to our blog directory to create another folder for comments and create package.json file to install the same as we did for the `posts`

        $ posts cd ..
        $ blog mkdir comments
        $ blog cd comments 
        $ comments npm init -y 
        $ comments npm install express cors axios nodemon


        