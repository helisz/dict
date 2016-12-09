# Project Startup I

## Gulp Configuration
1. Install gulp globally:
If you have previously installed a version of gulp globally, please run npm rm --global gulp to make sure your old version doesn't collide with gulp-cli.
`$ npm install --global gulp-cli`


2. Initialize your project directory:
`$ npm init`


3. Install gulp in your project devDependencies:
`$ npm install --save-dev gulp`


4. Create a gulpfile.js at the root of your project:
Gulpfile.js
```
'use strict';

var gulp 	= require('gulp');
var sass 	= require('gulp-sass');
var wiredep = require('wiredep').stream;

/** Wiredep - add bower dependencies to index.html **/
'use strict';

var gulp 	= require('gulp');
var wiredep = require('wiredep').stream;

/** Wiredep - add bower dependencies to index.html **/
gulp.task('bower', function () {
    gulp.src('../WEB-INF/jsp/home.jsp')
        .pipe(wiredep({
            optional: 'configuration',
            goes: 'here'
        }))
        .pipe(gulp.dest('../WEB-INF/jsp'));
});

/** tasks **/
gulp.task('default', ['bower']);
```

## Running Gulp.js tasks
1. `Settings` > `Tools` > `Startup Tasks` , find green `+`, add a Gulp.js task. 
2. `Gulpfile` need to be pointed to you gulpfile.js, and `Task` usually use `default`. Save and close.
3. Now on right top task runner dropdown you will find gulpfile as a stand-along task. Click green arrow to run it.


Each time use `$ bower install [NAME] --save`, run gulpfile task again to apply.