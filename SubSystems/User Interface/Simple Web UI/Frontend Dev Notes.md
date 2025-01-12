## Overview
We will most likely be using...
- [[React]] for the front end UI
	- React-Select for dropdown menus
- [[Axios]] for making HTTP requests to the backend
- [[Tailwind CSS]] or Material UI for styling
	- Might want to look into other styling options
	- Will use [shadcn/ui](https://ui.shadcn.com/)

## Initialize React Project
#### Install NPM
npx is an npm command. we need to install NPM first. NPM comes with Node.js, so let's install it from their websites recommended method:
1. Install Node Version Manager (nvm)
2. Use nvm to install Node.js
```bash
# Download and install nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash

# Download and install Node.js:
nvm install 22

# Verify the Node.js version:
node -v # Should print "v22.13.0".
nvm current # Should print "v22.13.0".

# Verify npm version:
npm -v # Should print "10.9.2".

```
#### Initialize React App
```bash
npx create-react-app frontend
cd frontend
npm install axios react-select
```

>[!info]- npx VS npm
> NPM = Install and run package
> NPX = Run the package but don't install it
> 
>One installs a package/dependency for your project, saves it under node_modules and also in the package.json, example: npm i express
>
> The other one "executes" the package, only for that run, and doesn't save anything anywhere, for example: npx create-react-app

##### IMPORTANT: VULNERABILITIES
You still need to address these 6 vulnerabilities at a later date: 
```
* **nth-check < 2.0.1 (high severity):** This vulnerability is related to inefficient regular expression complexity in `nth-check`. 
* **css-select <= 3.1.0 (depends on vulnerable nth-check):** This vulnerability is inherited from the dependency `nth-check`. 
* **svgo 1.0.0 - 1.3.2 (depends on vulnerable css-select):** This vulnerability is inherited from the dependency `css-select`. 
* **@svgr/plugin-svgo <= 5.5.0 (depends on vulnerable svgo):** This vulnerability is inherited from the dependency `svgo`. 
* **@svgr/webpack 4.0.0 - 5.5.0 (depends on vulnerable @svgr/plugin-svgo):** This vulnerability is inherited from the dependency `@svgr/plugin-svgo`. 
* **react-scripts >= 2.1.4 (depends on vulnerable @svgr/webpack and resolve-url-loader):** This vulnerability is inherited from the dependencies `@svgr/webpack` and `resolve-url-loader`. 
* **resolve-url-loader < 0.0.1-experiment-postcss || 3.0.0-alpha.1 - 4.0.0 (moderate severity):** This vulnerability is related to PostCSS line return parsing errors. 
* **postcss < 8.4.31 (moderate severity):** This vulnerability is also related to PostCSS line return parsing errors.
```

## Create REACT Components
Going to go with these techs
- **Tailwind CSS**: The base styling framework. It provides utility classes you use to style all components.
- **shadcn/ui**: A source of customizable, unstyled components that you can style with Tailwind. These will form the core of your application’s custom design system.
- **DaisyUI**: A helper library for prototyping with pre-styled components, speeding up the development process for less critical UI elements.

Installing dependencies...


---

#react #python #frontend #ui #research #development #restapi #rest #axios #css #style 