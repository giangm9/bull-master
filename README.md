# bull master [![NPM Version](https://img.shields.io/npm/v/bull-master)](https://www.npmjs.com/package/bull-master) [![NPM Downloads](https://img.shields.io/npm/dw/bull-master)](https://www.npmjs.com/package/bull-master) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com) [![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier) [![build](https://github.com/hans-lizihan/bull-master/workflows/Node%20CI/badge.svg)](https://github.com/hans-lizihan/bull-master/actions?query=workflow%3A%22Node+CI%22)

![Screen Shot bull-master](https://user-images.githubusercontent.com/7879022/77668840-e8e4ce80-6fbe-11ea-8a35-e65d247e10b6.png)

Bull Dashboard is a UI built on top of [Bull](https://github.com/OptimalBits/bull) to help you visualize your queues and their jobs.
With this library you get a beautiful UI for visualizing what's happening with each job in your queues, their status and some actions that will enable you to get the jobs done.

## Notes

As this library provides only the visualization for your queues, keep in mind that:

- You must have Bull installed in your projects;
- Aside the options to retry and clean jobs, this library is not responsible for processing the jobs, reporting progress or any other thing. This must be done in your application with your own logic;
- If you want to understand the possibilities you have with the queues please refer to [Bull's docs](https://optimalbits.github.io/bull/);
- This library doesn't hijack Bull's way of working.

If you want to learn more about queues and Redis: https://redis.io/.

## Starting

To add it to your project start by adding the library to your dependencies list:

```sh
yarn add bull-master
```

Or

```sh
npm i bull-master
```

## Hello World

The first step is to let bull-board know the queues you have already set up, to do so we use the `setQueues` method.

```js
// for express
const express = require('express')
const Queue = require('bull')
const bullMaster = require('bull-master')
const app = express()

const someQueue = new Queue()
const someOtherQueue = new Queue()

app.use('/admin/queues', bullMaster({
  queues: [someQueue, someOtherQueue],
}))

// for koa
const Koa = require('koa')
const Router = require('@koa/router')
const Queue = require('bull')
const bullMaster = require('bull-master')
const app = new Koa()

const someQueue = new Queue()
const someOtherQueue = new Queue()

router.all('/admin/queues*', bullMaster.koa({
  queues: [someQueue, someOtherQueue],
  prefix: '/admin/queues',
}))

app
  .use(router.routes())
  .use(router.allowedMethods())
// other configurations for your server
```

That's it! Now you can access the `/admin/queues` route and you will be able to monitor everything that is happening in your queues 😁

## Contributing

First of all, thank you for being interested in helping out, your time is always appreciated in every way. 💯

Remember to read the [Code of Conduct](https://github.com/hans-lizihan/bull-master/blob/master/CODE_OF_CONDUCT.md) so you also help maintaining a good Open source community around this project!

Here's some tips:

- Check the [issues page](https://github.com/hans-lizihan/bull-master/issues) for already opened issues (or maybe even closed ones) that might already address your question/bug/feature request.
- When opening a bug report provide as much information as you can, some things might be useful for helping debugging and understading the problem
  - Node, Redis, Bull, bull-board versions
  - Sample code that reproduces the problem
  - Some of your environment details
  - Framework you're using (Express, Koa, Hapi, etc).
- Feature requests are welcomed! Provide some details on why it would be helpful for you and others, explain how you're using bull-board and if possible even some screenshots if you are willing to mock something!

## Developing

If you want to help us solving the issues, be it a bug, a feature or a question, you might need to fork and clone this project.

To fork a project means you're going to have your own version of it under your own GitHub profile, you do it by clicking the "Fork" button on the top of any project's page on GitHub.

Cloning a project means downloading it to your local machine, you do it in the command line:

```sh
git clone git@github.com:YOUR_GITHUB_USERNAME/bull-master.git
```

That will create a `bull-master` folder inside the directory you executed the command, so you need to navigate inside it:

```sh
cd bull-master
```

_This project requires that you have [yarn](https://yarnpkg.com/lang/en/) installed_

Also make sure you are running Redis for this project (bull-master's example connects to Redis' default port 6379).

Now, to try it out locally you can run:

```sh
yarn --pure-lockfile 
yarn dev:client 
yarn dev:server
```

### Acknowledgements ❤️

- [Juan](https://github.com/joaomilho) for building the first version of this library
- [Vitor](https://github.com/vcapretz) this project is basically a radical rewrite from Vitor's [bull-board](https://github.com/vcapretz/bull-board) project

# License

This project is licensed under the [MIT License](https://github.com/hans-lizihan/bull-master/blob/master/LICENSE), so it means it's completely free to use and copy, but if you do fork this project with nice additions that we could have here, remember to send a PR 👍
