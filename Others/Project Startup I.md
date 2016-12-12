# Project Startup I

## Gulp Configuration
1. Install gulp globally:
If you have previously installed a version of gulp globally, please run npm rm --global gulp to make sure your old version doesn't collide with gulp-cli.
`$ npm install --global gulp-cli`


2. Initialize your project directory:
`$ npm init`


3. Install gulp in your project devDependencies:
```$ npm install --save-dev gulp```

4. Install wiredep in your project devDependencies:
```$ npm install --save wiredep```

5. Create a gulpfile.js at the root of your project:
Gulpfile.js
```javascript
'use strict';

var gulp 	= require('gulp');
var wiredep = require('wiredep').stream;

/** Wiredep - add bower dependencies to index.html **/
gulp.task('bower', function () {
    gulp.src('../WEB-INF/jsp/home.jsp')
        .pipe(wiredep({
            directory: './bower_components',
            ignorePath: '../../'
        }))
        .pipe(gulp.dest('../WEB-INF/jsp'));
});

/** tasks **/
gulp.task('default', ['bower']);
```

6. Running Gulp.js tasks
#### with Terminal
Use following command to execute the task
```
$ gulp [bower]
```
#### with Startup Tasks function in IntelliJ
1. `Settings` > `Tools` > `Startup Tasks` , find green `+`, add a Gulp.js task. 
2. `Gulpfile` need to be pointed to you gulpfile.js, and `Task` usually use `default`. Save and close.
3. Now on right top task runner dropdown you will find gulpfile as a stand-along task. Click green arrow to run it.

```
WHEN YOU ADD PLUGINS,
Each time use `$ bower install [NAME] --save`, run gulpfile task again to apply.
```

## SASS Configuration
#### Use Gulp.js
1. Intall gulp-sass
```
npm install gulp-sass --save-dev
```
2. Add following js code into `gulpfile.js`
```javascript
/** add dependency **/
var sass = require('gulp-sass');

/** gulp-sass **/
gulp.task('sass', function () {
    return gulp.src('./scss/*.scss')

        .pipe(sass({
                outputStyle: 'compressed'
            })
            .on('error', sass.logError)
        )
        .pipe(gulp.dest('./css'));
});

 gulp.task('sass:watch', function () {
     gulp.watch('./scss/*.scss', ['sass']);
 });

 /** append task after previous task 'bower' **/
gulp.task('default', ['bower', 'sass-watch']);
```
3. In terminal, call the task name:
```
$ gulp sass-watch
```
#### Use File Watcher in IntelliJ
1. `Settings` > `Tools` > `File Watchers`, click green `+`.
2. Add a scss watcher, config as follows: 
```
Program:		C:\Ruby23-x64\bin\scss.bat
Arguments:		--no-cache --update $ProjectFileDir$\WebContent\resources\scss:$ProjectFileDir$\WebContent\resources\css
Working Dir:	$ProjectFileDir$\WebContent\resources\scss
Env. Vars:		[EMPTY]
Output...: 		$ProjectFileDir$\WebContent\resources\css\$FileNameWithoutExtension$.css:$ProjectFileDir$\WebContent\resources\css\$FileNameWithoutExtension$.css.map
```
3. Save and make sure it is ticked. Follow this file structure:
```
resources
	└ bower_components
		└ [components_with_css]
			└ component-css1.scss
			└ component-css2.scss
	└ css
		└ style.css
	└ scss
		└ _custom1.scss
		└ _custom2.scss
		└ style.scss 
```
in `style.scss`:
```
// External Utilities
@import "../bower_components/[components_with_css]/component-css1.scss";
@import "../bower_components/[components_with_css]/component-css2.scss";

// Custom Classes
@import "custom1";
@import "custom1";
```

Each time you change anything in scss file, everything will be compiled to css/style.css