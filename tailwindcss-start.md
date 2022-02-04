## Getting Started with TailwindCSS

#

### Setup and Running

1.  Initiate package.json file

        $ npm init -y

2.  Installing dependency with frontend server and dev server `vite` with a flag `-D` for development dependency

        $ npm install -D tailwindcss postcss autoprefixer vite

3.  Modigying in 'package.json' to make `vite` command run with `dev` write under `script` like the following:

        "scripts": {
            "dev": "vite",
        },

4.  Adding Tailwind config file with a flag `-p` for postCSS enabled

        $ npx tailwindcss init -p

    This will create 2 files named `tailwind.config.js` and `postcss.config.js` for configure our own tailwind and poscss respectively

5.  Adding TailwindCSS

- Add a main CSS file

  Add `index.css` file in a directory like `assets/css` and add the following lines to use TailwindCSS

        @tailwind base;
        @tailwind components;
        @tailwind utilities;

- Compile the file having TailwindCSS style rules

        $ npx tailwindcss -i index.css -o dist/css/style.css

- Add CSS file into your index.html

        <link rel="stylesheet" href="/assets/css/style.css" />

6.  Run the server

        $ npm run dev

7.  Adding Tailwind Config Viewer `(https://github.com/rogden/tailwind-config-viewer)`.

- Installing Tailwind Config viewer

        $ npm i tailwind-config-viewer -D

- Configure script to run the viewer `"tw-viewer": "tailwind-config-viewer -o"`

        "scripts": {
            "dev": "vite",
            "show": "tailwind-config-viewer -o",
        }

- Run the viewer into the browser

        $ npm run show

- We can add a script to build or compile our CSS based on configuration (modifying the 5.2 command in Script)

        "scripts": {
            "dev": "vite",
            "show": "tailwind-config-viewer -o",
            "build:css": "npx tailwindcss -i index.css -o dist/css/style.css",
        }

8.  Adding Forms reset to apply style without any hassle (Ref: https://github.com/tailwindlabs/tailwindcss-forms)

    $ npm install @tailwindcss/forms

    Then add the plugin to your tailwind.config.js file:

        // tailwind.config.js
        module.exports = {
        theme: {
            // ...
        },
        plugins: [
            require('@tailwindcss/forms'),
            // ...
        ],
        }

9.  Then build your CSS:

        $ npm run build:css
