# react-component
> A simple development process for reuseable react components written in ES6.

## Assumptions
This repository gives you a starting point if you want to:
* develop reusable components independently
* use `browserify`
* write in ES6 using `babelify`
* use JSX
* write tests with [`tape`](https://github.com/substack/tape)
* maintain no separate css file, but use [inline styles](http://facebook.github.io/react/tips/inline-styles.html) with react
* use simple npm scripts to build, not Grunt or Gulp
* be able to understand the system and code in this boilerplate in 5 minutes

## Get started
Clone this repo, change the git origin to your repository, change package name (and version) in `package.json` and install:

```bash
git clone git@github.com:USERNAME/OTHERREPOSITORY.git
cd TK
git remote set-url origin git@github.com:USERNAME/OTHERREPOSITORY.git
vim package.json
npm install
```

You might also want to remove this README and write your own.

## Build process
You will most likely only need these one task:
`npm run serve`: sets up watchify and a livereload server; opens in your favorite browser

## 5-minute comprehension
So how does this build process work? Let's look at what the different files are for:
* `index.jsx`: This **is** your component, exported as a CommonJS module. You can use ES6 and JSX syntax.
* `test.js`: Tests for your component go here. You can use ES6 here as well.
* `index.html`: This is a simple html file used by the livereload server, to serve your component's JavaScript.

Remember: The only two files you should ever need to work on are `index.jsx` and `test.js`.

How is this wired up under the hood? All npm script "tasks" really just call node executables or run other npm scripts. For example, the `dist` task is running `browserify` and `uglifyjs` to compile your minified build. If you look at the "scripts" section in `package.json` you should have a pretty good understanding of which task is using which executable.

If we look at the `dist` task in detail, you can see that it first runs another npm script `ify`, which is browserifying the `index.jsx` file with the `babelify` transform.  The output of this is piped into `uglifyjs` which minifies to `dist/index.min.js`. Notice the `-s` flag after each `npm run`. It makes sure that npm doesn't print the commands themselves to stdout, which means you can keep piping output of npm scripts to other commands.
