# React Native with EXPO 
Ref: https://github.com/piyush-eon/react-native-course/

## Create project using NPM command (assuming that npm is installed)

    npm create expo-app todo

Then 

    cd todo
    npm run android
    npm run ios
    npm run web

## UI Library

    https://reactnative.dev/
    https://www.nativewind.dev/docs/getting-started/installation
    https://reactnativepaper.com/
    https://docs.expo.dev/router/advanced/native-tabs/

### Install CSS Library that powwered by TailwindCSS (Install NativeWind)

    npm install nativewind react-native-reanimated react-native-safe-area-context
    npm install --dev tailwindcss@^3.4.17 prettier-plugin-tailwindcss@^0.5.11 babel-preset-expo

### Initialize Tailwind CSS

    npx tailwindcss init

### Configure tailwind.config.js

    /** @type {import('tailwindcss').Config} */
    module.exports = {
    content: [
        "./App.{js,jsx,ts,tsx}",
        "./app/**/*.{js,jsx,ts,tsx}",
        "./components/**/*.{js,jsx,ts,tsx}",
    ],
    presets: [require("nativewind/preset")],
    theme: {
        extend: {},
    },
    plugins: [],
    };

### Create a file `touch babel.config.js` and copy the code below:

    /** @type {import('tailwindcss').Config} */
    module.exports = {
    content: [
        "./App.{js,jsx,ts,tsx}",
        "./app/**/*.{js,jsx,ts,tsx}",
        "./components/**/*.{js,jsx,ts,tsx}",
    ],
    presets: [require("nativewind/preset")],
    theme: {
        extend: {},
    },
    plugins: [],
    };

### Configure Metro (`touch metro.config.js`) and copy the code below:

    const { getDefaultConfig } = require("expo/metro-config");
    const { withNativeWind } = require("nativewind/metro");
    const config = getDefaultConfig(__dirname);
    module.exports = withNativeWind(config, { input: "./global.css" });

Now find the following section in `app.json` and add `"bundler": "metro",` like below: 

    "web": {
      "bundler": "metro", // --> this line
      "output": "static",
      "favicon": "./assets/images/favicon.png"
    },

### Create global CSS (`touch global.css`) and copy the code below:

    @tailwind base;
    @tailwind components;
    @tailwind utilities;

### TypeScript setup (`touch nativewind-env.d.ts`) copy the code below:

    /// <reference types="nativewind/types" />

### Update app/_layout.tsx and add the `global.css`

    import "../global.css";
    import { useFonts } from "expo-font";
    ... other code goes here

### Install this VSCode Extension: ES7+ React/Redux/React-Native snippets

## Add clerk for Email based authentication

### Setup clerk app and copy the `EXPO_PUBLIC_CLERK_PUBLISHABLE_KEY` and save to .env

Intall dependency

   npm install @clerk/expo expo-secure-store

