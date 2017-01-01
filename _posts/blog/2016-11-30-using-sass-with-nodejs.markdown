---
layout: post
title:  "Using sass with nodejs!"
modified:
categories: blog
excerpt:
tags: [sass,nodejs]
image:
  feature:
date:   2016-11-30 20:02:16 +1000
---
So I finally figured out how to use sass with nodejs! Something that took me an embarrassing amount of time to accomplish.

SASS is a CSS pre-processor that lets you write and manage stylesheets better. SASS lets you use variables, mixins, and nest elements. The sass stylesheets then get compiled into CSS.

This is the bit I struggled with the most in getting to work on my node server. I didn't know how to properly pre-process the sass files. I know there are multiple ways to do it, I looked at doing it natively with the sass gem, using node-sass and others.

I don't know if this is the best way, but the way I figured out how to do it was using something called grunt.

According to gruntjs.com, grunt is an automation task runner. It looks like it can do things like minifications, unit testing, pre-processing (obviously) and other things.

Here are the steps I had to follow to get sass properly pre-compiling:

1. After setting up my node server, I needed to install Grunt.
`$ npm install --save-dev grunt`

2. Create the public directory for the processed stylesheets to go in
`$ mkdir public/stylesheets`

3. I already had this bit done, but ensure the jade engine is setup properly
`$ npm install jade --save`
```
// views as directory for all template files
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'jade');
app.use(express.static('public'));
```

4. Install Grunt-Sass
'$ npm install --save-dev grunt-sass'

5. Make a new folder called "sass" in the root project directory

6. Create a file in the project root directory called gruntfile.js and add the following contents

```javascript
module.exports = function(grunt) {
  grunt.initConfig({
    sass: {
      dist: {
        files: {
          'public/stylesheets/style.css': 'sass/style.scss'
        }
      }
    },
    watch: {
      source: {
        files: ['sass/**/*.scss', 'views/**/*.jade'],
        tasks: ['sass']
      }
    }
  });

  grunt.loadNpmTasks('grunt-contrib-watch');
  grunt.loadNpmTasks('grunt-sass');
  grunt.registerTask('default', ['sass']);
};
```

7. Install Grunt Watch
`$ npm install grunt-contrib-watch --save-dev`

The resulting project directory structure should look something like this:

```
project-root
|- node_modules/
|- public/
|--- stylesheets/
|- sass/
|- views/
```

8. The best thing to do is to open three terminal windows. 
  1. In the first run `$ node server.js`
  2. In the second run: `$ grunt watch`
  3. The third terminal is for general file navigation