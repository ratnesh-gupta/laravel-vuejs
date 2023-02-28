
## About setup Vue 3 in Laravel 8

There are a few [options](https://laravel.com/docs/8.x/installation) when it comes to installing Laravel. We will be using Composer to setup the Laravel framework.

For this you will need to install the following:

[Composer](https://getcomposer.org/)

[Node](https://nodejs.org/en/)

And for development you will be needing PHP 8.

After installing all of this, we can simply run the following command to scaffold a complete Laravel project:

`composer create-project Laravel/laravel <app-name>`

## Install and configure Vue 3

If you have been using Laravel from 6.x onward, you may well have come across the Laravel/ui package, with which we could install Bootstrap as well as React or Vue.

For Vue 3 there is not a package as of time of writing, but there is a rather easy way of doing this.

Let us first install the dependencies needed for Vue 3:

`npm install --save vue@next && npm install --save-dev vue-loader@next`

## Laravel update Webpack.mix.js for Vue

```php
const mix = require("laravel-mix");

mix.js("resources/js/app.js", "public/js")
    .vue()  //<-- we need to make add vue() at this line  
    .postCss("resources/css/app.css", "public/css", [
        //
    ]);
```
I usually run `npm install` followed by `npm run dev` or you can use `npm run dev watch` as `watch` will allow you to see all changes and recomplie when ever you do any update in the webpack.mix.js file


## Running Laravel on local

With Laravel 8.x , we have got [Laravel Sail](https://laravel.com/docs/8.x/sail) , you can use this or we can you ``php artisan serve`` for running the Laravel project on local.


## Create our Vue project 

Let us change that by creating a root component that will house our entire Vue app.

- Create a new App.vue file in the resources/js folder with the following markup:
```html
<template>
    <div>
        <h1>Welcome to Laravel 8 + Vue js 3</h1>
        <h4>Testing page from Vue</h4>
    </div>
</template>
```
A very simple Vue app with a heading.


- Now we need to adapt our app.js in resources/js to make use of our vue file:
```javascript
//resources/js/app.js

import { createApp } from "vue";

import App from "./App.vue";

createApp(App).mount("#app");

require("./bootstrap");

```

Here we are first importing the createApp() method that is new to Vue developers. With this we can create a new Vue instance.

We then import our Vue file and create a new Vue instance and mount it on an element with the id "app".

Now let us create an element that has that id. To do this, we can remove the standard markup found in our welcome.blade.php file and replace it with this:

```html
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">

        <title>Laravel</title>

        <!-- Fonts -->
        <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700&display=swap" rel="stylesheet">
    </head>
    <body>
        <div id="app"></div>
    </body>
    <script src="{{ asset('js/app.js') }}"></script>
</html>
```
