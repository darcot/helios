Helios
=========

Initial Setup
-------------
1. Install node
 1. On Mac: `brew install node`
 1. On Windows: follow these [instructions](https://nodejs.org/en/)
1. Install global npm modules (grunt-cli, karma-cli, bower): `npm install -g grunt-cli karma-cli bower`
1. Change to the 'helios' directory
1. Install npm dependencies `npm install`
1. Install bower dependencies `bower install`
1. Make sure you have SaSS installed: `gem install sass -g`

Running the Application
-----------------------
You can run the application with [mocked](#dev-with-mocked-data) or [real](#dev-with-real-data) data.

### Dev with Mocked Data
This takes less time to setup and run but uses mock data.

Run `grunt mocks`
Open URL `http://localhost:8000/`

This serves the project files and the mocked backend data using [Connect](http://www.senchalabs.org/connect/).
It also hints, validates and runs tests on change.
To add/update a cd-backend mock, simply update the [test/mocks](./test/mocks) directory.

### Dev with Real Data
This takes more time to setup and run but emulates the real environment.

1. Setup [dev-environment](https://github.com/Accordance/dev-environment.git).
1. Change to the `helios` directory.
1. Run `grunt` to lint, validate and runs tests on change.
1. View the project at [http://localhost:8080](http://localhost:8080).

Development on the Application
------------------------------
The Helios project uses [Grunt](http://gruntjs.com) for asset management, unit testing, serving assets locally, and overall developer convenience.

### Summary
[Grunt](http://gruntjs.com) is a JavaScript task runner, not too different from Maven, Rake, Make, Gradle, etc.
Grunt is installed via [node package manager](https://www.npmjs.org/), which also handles dependency management for the project.
If you are new to Grunt, you should take a look at the [Grunt getting started guide](http://gruntjs.com/getting-started).

### Development
- Each time you pull new changes from `master` you should run `npm install && bower install` in the `helios` directory.
- You **MUST** have either `grunt mocks` or `grunt dev` active in your shell during front-end development.

#### Grunt Tasks
Below are a list of custom Grunt tasks. They are designed to make your life easier and your code better.

- `grunt`: Checks all files then produces a development build.
- `grunt dev`: Watches your project files and runs tests, hints, and validates on change.
- `grunt test`: Runs unit tests on JS files in Chrome.
- `grunt mocks`: Serves project files and cd-backend mocks. Also runs tests, hints, and validates on change.
- `grunt check`: Runs all checks for html, css, and js.
- `grunt release`: Creates a build for release.

The Build Pipeline
------------------
The [build pipeline](https://travis-ci.com/) is automatically kicked off when you
push a commit to the `master` branch of [helios](https://github.com/Accordance/helios).
Run all your checks (style and unit tests) locally via `grunt check` as the pipeline is dependent on these passing.

### Bumping versions
The pushed commits automatically bump the patch level of this repo.
The current checked in version is the expected *next* version of the app.
Because the version number lives in multiple locations, it is recommended to use:
`grunt bump::minor`
(or major) to increment the version for semantic versioning requirements.

Updating Dependencies
---------------------
Getting the latest and greatest shinny code is cool.
Here are some basic guidelines:

- Run all tests and perform a manual regression (as needed) before submitting a pull request.
- Specify the complete version of dependencies (i.e. no *, ~, and such).
This is to ensure a consistent experience for engineers and build servers.

### npm
npm's dependencies--defined in [package.json](./package.json)--are used by grunt to perform tasks.
To check for updates, run `npm outdated -depth=0`.
If you wish to update any NPM dependencies for the project, update [package.json](./package.json) accordingly and run `npm install`.

### Bower
Bower's dependencies--defined in [bower.json](./bower.json)--are used for front-end asset management.
To check for updates, run `bower list`.
If you wish to update any bower dependencies for the project, update [bower.json](./bower.json) accordingly and run `bower install`.
If Bower fails to download dependencies from git: but has success to download them via https: then you can apply the following command to tell git to do the substition for you:
```
git config --global url."https://".insteadOf git://
```

Notes
-----
* Angular Seed: https://github.com/angular/angular-seed
* Angular best practices: http://blog.artlogic.com/2013/05/02/ive-been-doing-it-wrong-part-1-of-3/

For issues with `npm install` (likely caused when on WiFi) try:
```bash
git config --global url."https://".insteadOf git://
```
Source: https://github.com/bower/bower/issues/50