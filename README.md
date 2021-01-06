# my-api-server

## How to setup a local and remote JSON REST API Server in ten-ish easy steps

### Intro

A few days ago I started working on a fun little project and quickly needed a test Rest API setup. As I have run into this a few times in the last few months I figured I'd come up with a solution once and for all!

#### Requirements

My requirements were pretty basic, I wanted something that I could quickly drop some json into and that created Rest end points on the fly. I also wanted to be able to run it locally and "online".

After some online research, I came across [My JSON Server](https://my-json-server.typicode.com), a "Fake Online REST server for teams". It is free and seems to do the online part!

All you need to is create a Repo on Github and add a JSON file named `db.json` with some content like this, or "whatever" json you like!


```
{
  "posts": [
    {
      "id": 1,
      "title": "Post 1"
    },
    {
      "id": 2,
      "title": "Post 2"
    },
    {
      "id": 3,
      "title": "Post 3"
    }
  ],
  "comments": [
    {
      "id": 1,
      "body": "some comment",
      "postId": 1
    },
    {
      "id": 2,
      "body": "some comment",
      "postId": 1
    }
  ],
  "profile": {
    "name": "typicode"
  }
}
```

Once you are done you can hit a URL like this [http://my-json-server.typicode.com/user/repo](http://my-json-server.typicode.com/user/repo), replacing 'user' with your username and 'repo' with the name of the repo you created and voila, your online REST API is there. You can now use Postman to test it to make sure you formatted that JSON right. Very cool!

![Postman](https://github.com/cashoefman/my-api-server/blob/main/images/Postman.png?raw=true)

But I also wanted to be able to run this local, so, lets get this setup. Instead of creating the repo online, this is how you set that up from the command line!

Note: This presumes you have GIT installed and working and the GIT CLI installed too. If not there are plenty of tutorials out there on how to do that.
```
mkdir ~/Projects/my-api-server
cd ~/Projects/my-api-server
npm init -y
npm install json-server
```
Now we need to add a db.json file, you can use the example I used above or create your own and we need to update the package.json file to look like this:
```
{
  "name": "api-server",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "json-server db.json"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "json-server": "^0.16.3"
  }
}
```
Now you can start the server locally by running 'npm start' in your terminal and if that all works as expected, we'll add the online part! 

To do that add a .gitignore file if it wasn't automatically created for you and exclude the node_modules, we don't need those in the repo and initialize the repo.
```
touch .gitignore
echo node_modules > .gitignore
git init .
```
Nex we''ll create the git repo, you can accept the defaults or modify it to your liking:
````
gh repo create -y
````
And finally we push everything to Github:
```
git add --all .
git commit -m "premiere"
git push origin main
```
Now you can go to: `https://my-json-server.typicode.com/<yourgitname>/my-api-server` to use the repo online or locally by running 'npm start' in your terminal.

![Postman](https://github.com/cashoefman/my-api-server/blob/main/images/Postman.png?raw=true)
How Cool Is That??
