# Basic sample

Let's start with a very basic sample, just add an html plus a simple console log (E5), what you can find in the getting started tutorial.

# Steps to build it

## Prerequisites

Install [Node.js and npm](https://nodejs.org/en/) (min v8.9) if they are not already installed on your computer.

> Verify that you are running at least node v8.x.x and npm 5.x.x by running `node -v` and `npm -v` in a terminal/console window. Older versions may produce errors.

## Steps

- Navigate to the folder where you are going to create the empty project.

- Execute `npm init`, you will be prompted to answer some information request
about the project (once you have successfully fullfilled them a **`package.json`**
file we will generated).

```bash
npm init -y
```

> Ensure your parent folder does not include spaces or uppercase (if that's the case you can just run _npm init_ and change
the project name).

- Let's install parcel 

```bash
npm install parcel-bundler --save-dev
```

- Let's create a basic index js file (es5 friendly):

_./src/index.js_

```javascript
console.log("hello parcel!");
```

- Let's create a dummy index.html file

_./src/index.html_

```html
<html>
<body>
  <script src="./index.js"></script>
  <h1>Check the console log</h1>
</body>
</html>
```

- Now let's add the following command tu our package.json

_package.json_

```diff
  "scripts": {
+   "build": "parcel ./src/index.html",  
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

- Let's run the build

```bash
npm run build
```

> A new folder will be generated _dist_ containing the bundled solution.

- What if we need a production ready version? let's add the following command
in our package.json:

_./package.json_

```diff
  "scripts": {
    "build": "parcel ./src/index.html",  
+    "build:prod": "parcel build ./src/index.html ",      
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

- Now if you run the command you will get a minified a version plus _NODE_ENV=production_

```diff
npm run build:prod
```

- There's a gotcha old files do not get erased, let's add the rim-raf plugin to ensure we are 
clearing up _dist_ folder before we generate the bundle.

```bash
npm install rim-raf --save-dev
```

- Let's add an extra step to the build process:

_package.json_

```diff
  "scripts": {
-    "build": "parcel ./src/index.html", 
+    "build": "rimraf dist && parcel ./src/index.html", 
-    "build:prod": "parcel build ./src/index.html",           
+    "build:prod": "rimraf dist && parcel build ./src/index.html",           
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

- Le't s run a lite web browser and check results:

_package.json_

```diff
  "scripts": {
    "build": "rimraf dist && parcel ./src/index.html", 
    "build:prod": "rimraf dist && parcel build ./src/index.html",           
+   "start": "rimraf dist && parcel ./src/index.html --open", 
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```

