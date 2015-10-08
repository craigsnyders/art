# AngularJS 1.4, TypeScript 1.6, RequireJS

## Core concepts
- [No Controllers](http://teropa.info/blog/2014/10/24/how-ive-improved-my-angular-apps-by-banning-ng-controller.html#comment-1660151019).  Only Components
- Components (aka Angular Directives) declare their own HTML & CSS
- Use TypeScript features as much as possible to get reasonably close to Angular2 code style
- Support minification (of JS and CSS)
- Support preloading concatenated CSS
- Support preloading of HTML templates [TODO]

## Installation
```javascript
npm install
bower install
http-server -p 8080
```
Note: serve the files however you like.  I chose [http-server](https://www.npmjs.com/package/http-server)

It should work from any context using relative paths, but is untested from anything except /

## Building the code
```bash
# transpile typescript
tsc

# create inline css file
grunt ngtemplates

# create minified .js file
grunt requirejs
```

## How?

RequireJS concatenates and minifies the javascript

CSS is dynamically loaded using Angular's $HTTP service, but it checks the $templateCache before resorting to $http. Grunt concatenates all component CSS files together by wrapping each template in a $templateCache.put(...) call.  This 1 file can then be loaded inside a module.run() block, so it executes before directives are instantiated.  
