# Building and Deploying a Website

What I did here is mainly what is showed in the codewithmosh HTML5/CSS3-Course Part 3 in the Videos _42 Building for Production_ and _44 Deployment_.

## Parcel - Setting up a Build Tool

### 1 Installing Node

First we need to install node in order to be able to install packages using _npm_.

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

The option **-g** means _global_ and allows us to execute parcel from any directory on our maschine instead of having to call it via _node_modules/.bin/parcel_.

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

This command is exactly like _parcel build_ but it also runs a webserver at http://localhost:1234 on the **dist/** folder.

When we deploy our website we want the server to automatically get the source code from our git-repository, then run parcel to make it ready for deployment and then publish those files.  
So the local use of parcel is to make sure everything works, but we also want to use parcel somewhere else automatically when deploying our website. This is where _Continuos Deployment_ Tools come into play.

## Netlify - Setting up a Continuous Deployment Tool

The following steps require you to have your git-repository on a **non**-self-hosted instance of Gitlab or Github

1. Get a Netlify-Account. It is also possible to login with Github or Gitlab.

2. Give Netlify read-Access to your repository.

3. Configure the Continuous Deployment in Netlify:

- Build Command: parcel build ./index.html
- Publish Directory: dist/

Netlify will then each time a new commit is detected in your remote repository on the specified branch launch a Linux-System, use package.json to install all dependencies (like Parcel) run the build command and then republish your website.  
The Publish Directory specifies the folder that the Web Server shall use as it's root directory. As the files that we want to deliver are stored into **dist/** by Parcel, we of course want to publish that directory.
