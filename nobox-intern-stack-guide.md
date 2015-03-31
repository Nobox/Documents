# Nobox Development 

## HTML

* Semantic HTML - Learn the concept of semantics and the semantic meaning of most HTML tags. Learn the main structure tags, `header`, `main`, `footer`, `section`, `aside`, etc. We write our HTML in the most semantic way possible.

* Advanced HTML5 forms: learn the new HTML5 `input` tags and their browser support, and how to change their styling in CSS and detect their values in JavaScript.

* Learn about the new HTML5 video element, the major supported video codecs on browsers and how to manipulate the video element with CSS.


## SVG

* Learn what [SVGs](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Introduction) are and their advantages over bitmaps.

* We use the [SVG symbols](https://css-tricks.com/svg-symbol-good-choice-icons/) spritesheet technique to hold all our SVGs. Learn more: [Icon system](https://css-tricks.com/svg-sprites-use-better-icon-fonts/), [External SVG file](https://css-tricks.com/svg-use-external-source/), and our [Elixir extension](https://github.com/waldemarfm/laravel-elixir-svg-symbols).

* See how SVG elements can be modified with CSS.


## CSS/Sass

* Understand the CSS box-model. Learn how the browser calculates dimensions by default with the default `content-box` box-model, and its difference with the `border-box` box model. All of our sites use the `border-box` box model so dimensions are calculated differently than normal. [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/box_model), [CSS Tricks](https://css-tricks.com/the-css-box-model/)

* Pseudo-elements, `::after` and `::before`. They are sprinkled throughout all of our projects, sometimes for really major visual elements.  Learn how to use them to minimize unsemantic markup for presentational purposes.

* The BEM class syntax. All of our CSS is written with BEM classes and looks fugly at first sight, so it's important you understand what's going on. [CSSWizardry](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

* Learn the basics of the Sass preprocessor, and what are mixins, functions and map lists.

* Our custom framework can be found at [Github](https://github.com/Nobox/beanie). It's a work in progress and may change its name, but it's being actively used for production projects. It's based on a bunch of [Inuitcss](https://github.com/inuitcss) components and some custom ones. It has no presentation whatsoever, but it's a solid foundation to start new projects from scratch.

* The structure, import order and names of all stylesheet files is based on the [ITCSS](http://csswizardry.net/talks/2014/11/itcss-dafed.pdf) architecture. [Inuitcss readme](https://github.com/inuitcss/getting-started#import-order)

* We adhere strictly to this master document of [CSS Guidelines](http://cssguidelin.es/)

* More important stuff
    * [When to use @extend; when to use a mixin](http://csswizardry.com/2014/11/when-to-use-extend-when-to-use-a-mixin/)
    * [The specificity graph](http://csswizardry.com/2014/10/the-specificity-graph/)
    

## JavaScript

* We are moving towards using vanilla JavaScript for most of our projects unless heavy DOM manipulation is required. This means we are moving away from jQuery. We're doing this because we believe JavaScript is the future and we want to understand it better, even if it's more tedious and will produce more lines of code. [You don't need jQuery](http://blog.garstasio.com/you-dont-need-jquery/), [You might not need jQuery](http://youmightnotneedjquery.com/)

* We're also using [ES6](https://babeljs.io/docs/learn-es6/) features like classes, template strings, and compiling our scripts with [Babel](https://babeljs.io/) to ES5.

* We use [Browserify](http://browserify.org/) to easily use npm modules for the browser. We use the [browserify-shim](https://github.com/thlorenz/browserify-shim) transform for compatibility of modules that are not CommonJS.


## Laravel

* We use the [Laravel](http://laravel.com/) PHP framework for most of our projects. We have a [custom starter app template](https://github.com/Nobox/laravel) that is the starting point for every project. For front-end development purposes, learn Laravel's [Blade templates](http://laravel.com/docs/5.0/templates), how to create a [route](http://laravel.com/docs/5.0/routing), a [controller](http://laravel.com/docs/5.0/controllers) method that is called through that route, and how to render a [view](http://laravel.com/docs/5.0/views#basic-usage) through a controller method.


## Tools

* We used Grunt once but moved to using the [Gulp]() task runner. We had written some custom Gulp tasks but now use Laravel 5's [Elixir](http://laravel.com/docs/5.0/elixir) gulp utility. A basic understanding of what is happening in our template app's `gulpfile.js` is recommended.

* We use [Bower](http://bower.io/) to easily install front-end dependencies that are not on npm.

* All of our projects have their own Git repo hosted on Github. We use a branch workflow with a `master` branch that has the production server code, and a `dev` branch that has the development server code. We push our code to the dev branch and solve any conflicts, and when it's ready to go live it's merged into the master branch and pushed. We also create additional branches as needed if major sets of features are being worked on for an app independently of the current app state.

* We currently use Digital Ocean droplets to host our sites and apps, managed through the [Laravel Forge](https://forge.laravel.com/) service. Forge has deployment hooks for repository branches that automatically run a deployment script on the server when code is pushed to the corresponding branch. For example, a project with the domain `dev.project.com` that is tracking the `dev` branch of a repo will automatically pull and run a deployment script whenever code is pushed to the Github remote branch. This is handy for our rapid development requirements.


## Culture

Our team is its own little world inside the agency, and our main focus is enjoying what we do to the maximum of our ability and keep learning our craft. It would be the greatest sin to turn complacent and think we know everything. This is an ever changing profession and to be the best we need to keep learning and improving.

### How you will feel with us

![](https://i.imgur.com/txNPc.gif)

### How we will treat you

![](https://i.imgur.com/4p9xz.gif)






