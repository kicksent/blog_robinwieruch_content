---
title: "How to setup MongoDB on MacOS"
description: "A installation guide for a MongoDB on MacOS setup for having a NoSQL database available on your OS. It comes with everything that's needed to connect a Node.js application to your database in JavaScript ..."
date: "2019-01-25T13:50:46+02:00"
categories: ["Node"]
keywords: ["mongodb macos", "mongodb setup", "mongodb os setup"]
hashtags: ["#NodeJs"]
banner: "./images/banner.jpg"
contribute: ""
author: ""
---

<Sponsorship />

This is a tutorial for setting up MongoDB on MacOS. You might be wondering why there's a need for another setup guide for MongoDB in the first place, since there are a few across the web. I found many tutorials and guides on how to set it up, but found most of them to be unclear and outdated, based on old MongoDB versions. The checklist is not comprehensive, though, as it is used for several tutorials on my website, I keep it updated with the recent versions of MongoDB. If you spot any flaws in this guide, a comment below would be very helpful to keep it up to date for other developers.

If you want to run MongoDB on Windows instead, you will find guidance over here: [How to setup MongoDB on Windows](https://www.robinwieruch.de/mongodb-windows-setup).

# MongoDB Installation on MacOS

I recommend [Homebrew](https://brew.sh/) for installing and managing applications on MacOS. It is installed using the following command in the MacOS terminal. Open up the terminal and paste the command:

```javascript
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

The terminal runs through a series of installation operations, and will probably create folders in your local machine to accommodate Homebrews storage requirements. After it's installed, add the custom tap using the command below. The tap makes it really simple to install the version you need. Once this is completed, you can install the latest version of mongodb with the second line. You can find more detailed instructions to install another version [here](https://github.com/mongodb/homebrew-brew). 

```
brew tap mongodb/brew
brew install mongodb-community
```

Now our data directory is ready with right permissions. Next run mongo daemon. Which is a service which runs in the background and listens for connections on a given port. Run this command:

```javascript
mongod
```

Now mongo daemon will be running in the background and can be used by your applications. Next, check your MongoDB version:

```javascript
mongo --version
```
Output:
```
MongoDB shell version v4.2.2
git version: a0bbbff6ada159e19298d37946ac8dc4b497eadf
allocator: system
modules: none
build environment:
    distarch: x86_64
    target_arch: x86_64
```

The command line results will show the version you have installed on your local machine. I recommend using the latest version of libraries and software whenever possible to avoid compatibility issues with client-side applications.

<ReadMore label="MongoDB with Mongoose in Express Tutorial" link="https://www.robinwieruch.de/mongodb-express-setup-tutorial" />
