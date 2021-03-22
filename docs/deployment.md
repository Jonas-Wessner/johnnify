# Building and Deploying a Website
What I did here is mainly what is showed in the codewithmosh HTML5/CSS3-Course Part 3 in the Videos *42 Building for Production* and *44 Deployment*.

## Parcel - Setting up a Build Tool

### 1 Installing Node
First we need to install node in order to be able to install packages using *npm*.

To check if you have installed Node properly type in the terminal:
```
$ node -v
```

### 2 Initialize npm-package in the directory
1. Open a terminal in the root directory of the project
2. 
```
$ npm init -y
```
Now we have created a new file named **package.json** in this directory that holds information about our project.

### 3 Install Parcel
```
$ npm i -D parcel-bundler
```
This installes parcel globally and adds the following to the **package.json** file (obviously the version might differ):
```json
"devDependencies": {
    "parcel-bundler": "^1.12.5"
  }
```
The option **-g** means *global* and allows us to execute parcel from any directory on our maschine instead of having to call it via *node_modules/.bin/parcel*.

### 4 Update .gitignore
These directories should be included in the **.gitignore**:
```makefile
# 3rd party libraries
node_modules/
# created when parcel builds the project
dist/
.cache/
```

### 5 Using Parcel
```
$ parcel build ./index.html
```
This command builds your project and puts all the files in the directory **dist/**.  
Parcel minifies the project by removing all comments white-spaces and so on.  
It also adds a random suffix to the names of our images in order to prevent browsers from caching this file and not reloading changes to our website properly.
So this **dist/** is the actual folder that we want to deploy.

```
$ parcel ./index.html
```
This command is exactly like *parcel build* but it also runs a webserver at http://localhost:1234 on the **dist/** folder.

When we deploy our website we want the server to automatically get the source code from our git-repository, then run parcel to make it ready for deployment and then publish those files.  
So the local use of parcel is to make sure everything works, but we also want to use parcel somewhere else automatically when deploying our website. This is where *Continuos Deployment* Tools come into play.

## Netlify - Setting up a Continuous Deployment Tool
