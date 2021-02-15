## React
  
###### install `yarn`
```
npm install --global yarn
```
  
###### check `yarn version`
```
yarn --verion
```
  
###### install `create-react-app`
```
yarn global add create-react-app
```
  
###### create `react web application`
```sh
yarn create react-app [project-name]
```
  
###### run `react web application`
```sh
yarn start
```
  
###### yarn simple guide & command
```sh
# Starts the development server.
yarn start
    
# Bundles the app into static files for production.
yarn build

# Starts the test runner.
yarn test

# Removes this tool and copies build dependencies, configuration files
# and scripts into the app directory. If you do this, you can’t go back!
yarn eject
   

# We suggest that you begin by typing:
cd [project-directory]
yarn start
```
  
###### how to set alias path `(for VSCode)`
```sh
# step 1
# add jsconfig.json

# step 2
# add config-overrides.js
  
# step 2.5
# keep webpack.config.js
  
# step 3
# install react-app-rewired --save-dev

# step 4
# modify package.json
```
  
###### `jsconfig.json`
```json
{
	"compilerOptions": {
		"baseUrl": ".",
		"paths": {
			"@/*": ["src/*"]
		}
	}
}
```
  
###### `config-overrides.js`
```js
const path = require("path");

module.exports = (config, env) => {
	config.resolve.alias = {
		"@": path.resolve(__dirname, "src"),
	};

	return config;
};
```
  
###### `webpack.config.js`
```js
const path = require("path");

module.exports = {
	resolve: {
		alias: {
			"@": path.resolve(__dirname, "src"),
		},
	},
};
```
  
###### `package.json`
```json
"scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test",
    "eject": "react-scripts eject"
},
```
  
###### `install sass(scss) loader`
```sh
yarn add node-sass --save
```
  
