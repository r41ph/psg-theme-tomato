# psg-theme-tomato

Theme for the [postcss-style-guide](https://github.com/morishitter/postcss-style-guide) plugin

## Install

```javascript
$ npm install psg-theme-tomato
```
## Example
GULP
```javascript
var gulp = require('gulp');
var sourcemaps = require('gulp-sourcemaps');
var postcss = require('gulp-postcss');
var minifyCSS = require('gulp-clean-css');
var rename = require("gulp-rename");
var sass = require('gulp-sass');
var styleGuide = require('postcss-style-guide');

// Transpiling scss
gulp.task('css', () => {
    console.log("Transpiling scss, etc...");
    return gulp.src('./*.scss')
        .pipe(sourcemaps.init())
        .pipe(sass().on('error', sass.logError))
        .pipe(postcss([
            styleGuide({
                project: 'Project name',
                dest: 'styleguide/index.html',
                showCode: true,
                theme: 'tomato' // => Add name of the theme here
            })
        ]))
        .pipe(minifyCSS({compatibility: 'ie8'}))
        .pipe(rename({
          suffix: '.min'
        }))
        .pipe(sourcemaps.write('.'))
        .pipe(gulp.dest('./dist/css/'));
});

gulp.task('watch', () => {
    gulp.watch('./*.scss', ['css']);
});

gulp.task('default', ['css']);
```
CSS - SCSS
```css
// Color palette
// No need of using Markup here, it can generate the 
// color palette from CSS Custom Properties with 
// @start color and @end color annotations.
$color-primary: #2E294E;
$color-secondary: #EFBCD5;
$color-tertiary: #BE97C6;
$color-background: #8661C1;
/* @start color */
:root {
    --primary: $color-primary;
    --secondary: $color-secondary;
    --tertiary: $color-tertiary;
    --background: $color-background;
}
/* @end color */


/*
@styleguide
@title Buttons
Use the button classes on and `<a>`, `<button>`, `<input>` elements.
#### => Sizes
<button class="button-large">button-large</button><br>
<button class="button-medium">button-medium</button><br>
<button class="button-small">button-small</button>
    <button class="button-large">button-large</button>
    <button class="button-medium">button-medium</button>
    <button class="button-small">button-small</button>
*/

.button {
	display: block;
    cursor: pointer;
    border: none;
    color: #fff;
    background-color: #999;

    &:hover {
    	opacity: .8;
    }
}

.button-large {
	@extend .button;
    padding: 20px 30px;
    font-size: 16px;
}

.button-medium {
	@extend .button;
    padding: 10px 20px;
    font-size: 14px;
}

.button-small {
	@extend .button;
    padding: 5px 10px;
    font-size: 12px;
}

```

## Theme

![Image of psg-theme-tomato](./psg-theme-tomato.png)

## License

MIT
