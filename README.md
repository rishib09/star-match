I followed the steps mentioned in the following link to create the react environment locally: 
        https://jscomplete.com/learn/1rd-reactful 

Please download Node.js and Visual Studio code for this project

Run the following commands in cmd or terminal or linux shell for the setup:
1. Run these to confirm the successful download of node.js:  
  a. node -v  
  b. npm -v  
  c. npx -v  
2. Go to your desired folder (Git enabled) and run the following commands:  
   a. npm init -y (it will install package.json in your folder)  
   b. Install the following dependencies :  
     i. npm i express (used for dynamic server rendering -- will install node_modules folder)  
     ii. npm i react react-dom (use these protocols to bundle packages in development and push it to production ---> not used in this project)  
     iii. npm i webpack webpack-cli (use to bundle all the modules(files under component) together)  
     iv. npm i babel-loader @babel/core @babel/node @babel/preset-env @babel/preset-react (Babel is used to convert JSX and modern js components to executable code used by webpack -- needs to be configured)  
     v. npm i -D nodemon (used as a node monitor in case of code updates there is no need to refresh the node)  
     vi. npm i -D eslint @babel/eslint-parser eslint-plugin-react eslint-plugin-react-hooks (Code Quality Tool)
     vii. npm i -D jest babel-jest react-test-renderer (testing tool)
  
   c. Create .eslintrc.js under the root folder  
     module.exports = {
      parser: "@babel/eslint-parser",
      env: {
        browser: true,
        commonjs: true,
        es6: true,
        node: true,
        jest: true,
      },
      parserOptions: {
        ecmaVersion: 2020,
        ecmaFeatures: {
          impliedStrict: true,
          jsx: true,
        },
        sourceType: "module",
      },
      plugins: ["react", "react-hooks"],
      extends: [
        "eslint:recommended",
        "plugin:react/recommended",
        "plugin:react-hooks/recommended",
      ],
      settings: {
        react: {
          version: "detect",
        },
      },
      rules: {
        "react/prop-types": "off",
        "react/react-in-jsx-scope": "off",
    
        // You can do more rule customizations here...
      },
    };

   ---> Initial Directory structure should look like the following:  
   baseFolder/   
      dist/  
          main.js  
      src/  
         index.js  
      components/  
         app.js  
      server/  
        server.js  

---> Configuring Webpack and Babel:
Create babel.config.js under root of the project folder with the following commands:

module.exports = {
  presets: [
    "@babel/preset-env",
    ["@babel/preset-react", { "runtime": "automatic" }]
  ],
};

Create webpack.config.js under root of the project folder with the following commands:

module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
        },
      },
    ],
  },
};

---> Create npm scripts for development
Under package.json, you will find a key 
scripts:{
    "test" : "jest"
}

please add the following lines:
--In package.json
scripts: {
  "test": "jest",
  "dev:server": "nodemon --exec babel-node src/server/server.js --ignore dist/",
  "dev:bundler": "webpack -w --mode=development"
}