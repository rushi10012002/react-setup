## Introduction

Today we are going to make our life easier a little bit! As developers, we have to work in a team (in most cases). Different person has different styles, so it’s hard to follow a specific coding pattern. Also, some people like four spaces as a tab, and some like 2. So code format also looks weird if there are no specific rules. Today we are going to fix the problem together. Let’s enforce a coding style using eslint and format our code automatically using prettier!

## Motivation

There is a reason why I’m writing this blog. I learned to program from tutorials (mostly udemy ones)! I never saw anyone is showing how to add eslint/prettier anywhere. But I learned about it while working with a side project (as freelance work). Around 2020 I was getting a good amount of leads from Fiverr to work. But it was hard for me to work on the projects because I started my current full-time. So, I took the help of my friend, and honestly, the code he wrote looks bad formatted and does not properly follow any coding styles. I always used eslint & prettier in my vscode, so I never faced this issue about formatting & following coding styles. But I wasn’t really interested in setup his IDE because it’s not something I can force on someone. Then I learned about eslint & prettier more. I made a setup, which helped me gain what I was trying too hard to get. It made my life so easier. After setting up both, I never saw terrible formatting in the app, and minor issues like not using any variables are gone! This is why I’m showing this to you. Maybe it’ll save a lot of time for you! If this helps, share it with a person who needs this. Let’s make the dev team strong with knowledge sharing! But before that, lets jump into the next section –

## Things I’m using

*   Visual studio code
*   nodejs
*   create react app
*   npm packages
    *   eslint
    *   prettier
    *   eslint-plugin-prettier
    *   husky
    *   lint-staged

## Basic React app

We’ll start with a basic React app, and we’ll use [create-react-app](https://create-react-app.dev/) –  
`bash npx create-react-app your-app-name`  

This will be a react app and we’re not going to change anything because this tutorial is not related to reactjs. 

We’re going to work directly on the next step! The more straightforward step of this tutorial is prettier. So let’s dive into it!

## Prettier

We use prettier to auto-format our code. This saves a lot of time for me. I’ve also installed a vscode extension, which helps me a lot. So let’s install it.

```plaintext
npm i prettier -D
```

We’re using a -D for only installing it as dev dependencies. We don’t need to send this into our build. Once it is installed, let’s try to format our code with prettier. But to do that, we need to create a prettier config file. Because prettier doesn’t know how to format our codes, let’s create that file. It’ll be on our root folder, and the file name will be `.prettierrc`.

```plaintext
{ "trailingComma": "es5", "tabWidth": 2, "semi": false, "singleQuote": true }
```

You can configure a lot of things with it. [Click here](https://prettier.io/docs/en/configuration.html) to find out more. But We’re going with a simple configuration. I like tabWidth two spaces, and I don’t like semicolons much. All will be handled using prettier now. Isn’t this awesome???

## Eslint

Eslint helps us to enforce a coding style. You can define your own coding style. Mostly I use [airbnb style](https://github.com/airbnb/javascript/tree/master/react). So let’s install it. But if you have time, read the rules from [eslint website](https://eslint.org/docs/rules/) –

```plaintext
npm i eslint -D
```

Sadly it’s not going to end here. You need to create a config file for eslint. There are two ways to do it; you can do it by

*   Eslint
*   Manual

I prefer to use Eslint and I’ll show that way because it’s easier. Let’s start the process by typing –

```plaintext
./node_modules/.bin/eslint --init
```

Then it’ll popup

```plaintext
? How would you like to use ESLint? ...
  To check syntax only
  To check syntax and find problems
> To check syntax, find problems, and enforce code style
```

I’ll choose `To check syntax, find problems, and enforce code style` because I want to check syntax, find problems, and enforce code style! Then it’ll show –

```plaintext
? What type of modules does your project use? ...
> JavaScript modules (import/export)
  CommonJS (require/exports)
  None of these
```

I’ll choose `Javascript modules (import/export)` because I want to use import/export, not the old require/exports. Select and then –

```plaintext
? Which framework does your project use? ...
> React
  Vue.js
  None of these
```

Choose the framework you are using, and this is a dumb question, right? We’re using this inside reactjs. Let’s select that –

```plaintext
? Does your project use TypeScript? » No / Yes
```

We’re not using Typescript so let’s click at no! Then it’ll show –

```plaintext
? Where does your code run? ...  (Press <space> to select, <a> to toggle all, <i> to invert selection)
√ Browser
√ Node
```

We’ll use the browser to check the results, so select and –

```plaintext
? How would you like to define a style for your project? ...
> Use a popular style guide
  Answer questions about your style
```

I’ll choose the `Use a popular style guide` one. Because that’s easy to install and many developers already know about it. But if you want manual styles, just go with the `Answer questions about your style` option. Let’s select it –

```plaintext
? Which style guide do you want to follow? ...
> Airbnb: https://github.com/airbnb/javascript
  Standard: https://github.com/standard/standard
  Google: https://github.com/google/eslint-config-google
  XO: https://github.com/xojs/eslint-config-xo
```

There are a few style guides already. I choose `airbnb` most of the time. Go with the one you like!

```plaintext
What format do you want your config file to be in? ...
> JavaScript
  YAML
  JSON
```

I normally just choose `JSON` because it’s the easiest to read. But you can choose whatever you like too!

```plaintext
Checking peerDependencies of eslint-config-airbnb@latest
Local ESLint installation not found.
The config that you've selected requires the following dependencies:

eslint-plugin-react@^7.28.0 eslint-config-airbnb@latest eslint@^7.32.0 || ^8.2.0 eslint-plugin-import@^2.25.3 eslint-plugin-jsx-a11y@^6.5.1 eslint-plugin-react-hooks@^4.3.0
? Would you like to install them now with npm? » No / Yes
```

Let’s install the packages now! It’ll take a little bit of time. Finally, we’ll see the `.eslintrc.json` file! Have a first look at it.

Our eslint setup is done, but it will not work with prettier well. We need to do some more configuration to enable both to work together!

## Configure eslint & prettier together

This section also starts with installing an npm package called `eslint-plugin-prettier`, which will help us configure eslint and prettier together. We’ll install it with –

```plaintext
npm i eslint-plugin-prettier -D
```

We need to add this plugin inside `.eslintrc.json` file –

```plaintext
{
    "env": {
        "browser": true,
        "es2021": true
    },
    "extends": [
        "plugin:react/recommended",
        "airbnb"
    ],
    "parserOptions": {
        "ecmaFeatures": {
            "jsx": true
        },
        "ecmaVersion": "latest",
        "sourceType": "module"
    },
    "plugins": [
        "react", "prettier"
    ],
    "rules": {
      "semi": 0,
      "comma-dangle": 0,
      "prettier/prettier": "error",
      "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }]
    }
}
```

I updated the last two-part – `plugins` and `rules`. This will help us to work prettier and eslint together. Don’t worry; there is no more configuration needed for eslint and prettier.

Also, let’s add two scripts to our `package.json` file. This will help us to lint files by `npm run lint` and format our code by `npm run pretty` –

```plaintext
 "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "lint": "eslint --fix",
    "pretty": "prettier --write ."
  }
```

One quick note: In your project, maybe some files you don’t want to lint or format. So you can add them to `.eslintignore` file –

```plaintext
node_modules
public
build
```

For the ignore format, you can use `.prettierignore`

```plaintext
# Ignore artifacts:
build
coverage

# Ignore all HTML files:
*.html
```

But there is still a problem remaining. This all will work if you use an IDE with extensions like – eslint & prettier. Without it’ll not format automatically. We can force it by using `script` in `package.json` file. But let’s find a better solution!

## Husky

To force our coding style & format, we will use git hook. So that if anyone commits any code, it runs some linting and check if there is any issue with it. For this, we’re going to use `husky` and `lint-staged` –

```plaintext
npm i husky lint-staged -D
```

This will just install the package. But for using `lint-staged` we need to edit our `package.json` file. Let’s add some lines –

```plaintext
 "lint-staged": {
  "**/*.{js,jsx}": [
    "npm run lint",
    "prettier --write"
  ]
 }
```

With these four lines, we are just linting and formatting our code. But it’s not called from anywhere now. So we need to call it from somewhere. But before that, we need to install husky properly to run it –

```plaintext
npx husky-init && npm install
```

This will create a folder called `.husky` and inside it a file called `pre-commit` which will run `npm test` before committing. But for the current project, we don’t want to run the `npm test`, so we are going to change it into –

```plaintext
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

# npm test
npx lint-staged
```

Now we can try committing in git, and it’ll show us if there is an error! Now we are finally ready to test our project!

## Result and Testing

We’ll not explore the git today with this tutorial. Because git is a big topic and that needs another blog. You can quickly do a crash course on the git. Then came back here to see what I was doing from this point. First, I’ll change a little bit on the `app.js` file; going to add an extra line that we don’t need (Just to showcase what we have done so far)

```plaintext
import React from 'react'
import logo from './logo.svg'
import './App.css'

function App() {
  const tempVar = 5

  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit
          <code>src/App.js</code>
          and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  )
}

export default App
```

I just added the `const tempVar = 5` after the function, and let’s try to commit this into the github repo. I’m using

```plaintext
git add .
git commit -m "Initial Commit"
```

Now I’m getting an error.

```plaintext
[STARTED] Preparing lint-staged...
[SUCCESS] Preparing lint-staged...
[STARTED] Running tasks for staged files...
[STARTED] package.json — 10 files
[STARTED] **/*.{js,jsx} — 2 files
[STARTED] npm run lint
[FAILED] npm run lint [FAILED]
[FAILED] npm run lint [FAILED]
[SUCCESS] Running tasks for staged files...
[STARTED] Applying modifications from tasks...
[SKIPPED] Skipped because of errors from tasks.
[STARTED] Reverting to original state because of errors...
[SUCCESS] Reverting to original state because of errors...
[STARTED] Cleaning up temporary files...
[SUCCESS] Cleaning up temporary files...

✖ npm run lint:
npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! react-eslint-prettier@0.1.0 lint: `eslint --fix "C:/Users/demo/Desktop/nerdworks/Blogs Examples/react-eslint-prettier/src/App.js" "C:/Users/demo/Desktop/nerdworks/Blogs Examples/react-eslint-prettier/src/index.js"`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the react-eslint-prettier@0.1.0 lint script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     C:\Users\demo\AppData\Roaming\npm-cache\_logs\2022-02-18T18_07_55_543Z-debug.log

> react-eslint-prettier@0.1.0 lint C:\Users\demo\Desktop\nerdworks\Blogs Examples\react-eslint-prettier
> eslint --fix "C:/Users/demo/Desktop/nerdworks/Blogs Examples/react-eslint-prettier/src/App.js" "C:/Users/demo/Desktop/nerdworks/Blogs Examples/react-eslint-prettier/src/index.js"


C:\Users\demo\Desktop\nerdworks\Blogs Examples\react-eslint-prettier\src\App.js
  6:9  error  'tempVar' is assigned a value but never used  no-unused-vars

✖ 1 problem (1 error, 0 warnings)

husky - pre-commit hook exited with code 1 (error)
```

Maybe it’ll look overwhelming at first. But if you read from last, you’ll understand what we are doing here. Here the problem is showing on.

```plaintext
6:9  error  'tempVar' is assigned a value but never used  no-unused-vars
```

So that tempVar we created is creating an issue. Why? Because we are not using this variable. So just delete this and try to commit again. This time it’ll just work fine –

```plaintext
STARTED] Preparing lint-staged...
[SUCCESS] Preparing lint-staged...
[STARTED] Running tasks for staged files...
[STARTED] package.json — 10 files
[STARTED] **/*.{js,jsx} — 2 files
[STARTED] npm run lint
[SUCCESS] npm run lint
[STARTED] prettier --write
[SUCCESS] prettier --write
[SUCCESS] **/*.{js,jsx} — 2 files
[SUCCESS] package.json — 10 files
[SUCCESS] Running tasks for staged files...
[STARTED] Applying modifications from tasks...
[SUCCESS] Applying modifications from tasks...
[STARTED] Cleaning up temporary files...
[SUCCESS] Cleaning up temporary files...
[master 205b14e] Initial Commit
13 files changed, 449 insertions(+), 119 deletions(-)
 create mode 100644 .eslintignore
 create mode 100644 .eslintrc.json
 create mode 100644 .husky/pre-commit
 create mode 100644 .prettierignore
 create mode 100644 .prettierrc
 rewrite README.md (99%)
 delete mode 100644 src/App.test.js
 rewrite src/index.js (78%)
 delete mode 100644 src/reportWebVitals.js
 delete mode 100644 src/setupTests.js
```

This way, all the files will be used eslint & prettier before going to our GitHub repository!