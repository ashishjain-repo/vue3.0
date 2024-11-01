# Using Vue with CDN
Create a `index.html` file and the script tag from the vuejs.org for CDN place it in your html and then open a script tag and create vue app inside. The vue app contains the method data which returns an object and then we can mount that object to our  html with id or class, and can use template script `{{object-key}}` with object key which will return the value of the key pair. We can also create an eveny on something like a button like this `@eventName="methodName"`. To create that method we have to go under the data method in the app and create an object of method and then create a function inside of it. We can also access the objects returned by data using this keyword and access it in the methods.
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VUE Test</title>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{message}}</h1>
        <button @click="clickMe">Click Me</button>
    </div>
    <script>
        const app = Vue.createApp({
            data(){
                return {
                    message: "Hello From Vue"
                };
            },
            methods: {
                clickMe(){
                    console.log('Button Clicked');
                    this.message = "Updated Message";
                },
            },
        })
        app.mount('#app');
    </script>
</body>
</html>
```

# Create Vue application using NPM
To create an application using npm use this command `npm create vue@latest project-name`. After adding additional libraries or not get into that project and use `npm install` and then `npm run dev` to run the app.

# App starting Points
`App.vue` is the starting point of the application. We use `<template></template>` tags to pass the html content inside in which we can use the variables and Vue direcives in the tags. First we have to open a `<script>` tag at the top of the file and in the always to `export default` then inside use function data which will return objects. For the templateing in between template tags use `{{}}` and the directives that you can use goes in the tag attributes section something like this: `<p v-if="variable"></p>`. All the directives in vue start with `v-`.

# Example of if_else-if_else ladder directives
Assume that the variable that is coming from the data return is called status.
```
<p v-if="status === 'active'">User is Active</p>
<p v-else-if="status === 'pending'">User is Pending</p>
<p v-else>User is In-Active</p>

```

# Example of for loop directives
Assume that the variable that is comming from data return is called tasks which is an object
```
<h3>Tasks: </h3>
<ul>
    <li v-for="task in tasks" :key="task.id">{{ task.name }}</li>
</ul>
```
In this the key represent the unique identifier for each value.

# Example of bind directive
This directive help you to bind some data to an attribute. Lets assume we have a variable that contains the link to some external website.
```
<a v-bind:href="link">Click Me</a>
```
We have to put v-bind: and then the name of the attribute to bind that value to an attribute.
We can also leave it the following way
```
<a :href="link">Click Me</a>
```
This will work perfectly, without the v-bind, we just have to make sure to add the colon before the attribute which tells the complier that we will be using the dynamic value.

# Example of on event directive
This directive is use to put events on the elements, for example: we can put an event on a button to toggle something. There are two methds to achieve this.
```
<button v-on:click="toggleSomething">Toggle</button>
<button @click="toggleSomething">Toggle</button>
```