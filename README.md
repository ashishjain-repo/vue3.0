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

# Option API
Options API is the way where we can generate dynamic content using the data and returning the object and methods after data to create functions.

## Example of if_else-if_else ladder directives
Assume that the variable that is coming from the data return is called status.
```
<p v-if="status === 'active'">User is Active</p>
<p v-else-if="status === 'pending'">User is Pending</p>
<p v-else>User is In-Active</p>

```

## Example of for loop directives
Assume that the variable that is comming from data return is called tasks which is an object
```
<h3>Tasks: </h3>
<ul>
    <li v-for="task in tasks" :key="task.id">{{ task.name }}</li>
</ul>
```
In this the key represent the unique identifier for each value.

## Example of bind directive
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

## Example of on event directive
This directive is use to put events on the elements, for example: we can put an event on a button to toggle something. There are two methds to achieve this.
```
<button v-on:click="toggleSomething">Toggle</button>
<button @click="toggleSomething">Toggle</button>
```

# Composition API
## Setup
In Composition API we have to wrap our content like variables and methods inside of it. And to make it reactive in our html tags, we have to wrap the content inside the variables into ref for which we can import ref like this: `import {ref} from 'vue';`. Then when you declare variable you can wrap the value inside the ref method. When we are using reactive content, intead of using this keyword to refer to the varibale, we have have to use `variable.value` to get the value of the variable.

# Composition API vs Option API
- Composition API
```
<script>
  import { ref } from 'vue';
export default{
  setup()
  {
    const name = ref('John Doe');
    const status = ref('Active');
    const tasks = ref(['Task One', 'Task Two', 'Task Three']);
    const link = ref("https://google.com");

    const toggleStatus = () => 
    {
      if (status.value === 'active') {
        status.value = 'pending';
      }
      else if (status.value === 'pending') {
        status.value = 'inactive'
      }
      else {
        status.value = 'active'
      };
    };
    return {name, status, tasks, link, toggleStatus,}
  }
}
  
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is Active</p>
  <p v-else-if="status === 'pending'">User is Pending</p>
  <p v-else>User is In-Active</p>

  <h3>Tasks: </h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
    <a v-bind:href="link">Click Link</a>
    <a :href="link">Click Link</a>
  </ul>

  <button v-on:click="toggleStatus">Change Status</button>
  <button @click="toggleStatus">Change Status</button>
</template>
```
- Option API
```
<script>
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'pending',
      tasks: ['Task One', 'Task Two', 'Task Three'],
      link: "https://google.com",
    };
  },
  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        this.status = 'pending';
      }
      else if (this.status === 'pending') {
        this.status = 'inactive'
      }
      else {
        this.status = 'active'
      }
    },
  }
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is Active</p>
  <p v-else-if="status === 'pending'">User is Pending</p>
  <p v-else>User is In-Active</p>

  <h3>Tasks: </h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
    <a v-bind:href="link">Click Link</a>
    <a :href="link">Click Link</a>
  </ul>

  <button v-on:click="toggleStatus">Change Status</button>
  <button @click="toggleStatus">Change Status</button>
</template>
```

# Composition API - Short Way
We can remove the setip function and put setup in the script tag and we can also remove the export default from the script. We are also not required to return anything since we do not have an explicit setup. The code will look something like this and still will be functional and more readable: -
```
<script setup>

import { ref } from 'vue';

const name = ref('John Doe');
const status = ref('Active');
const tasks = ref(['Task One', 'Task Two', 'Task Three']);
const link = ref("https://google.com");

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  }
  else if (status.value === 'pending') {
    status.value = 'inactive'
  }
  else {
    status.value = 'active'
  };
};


</script>
```

## Forms and v-model
In the forms we can bind them with a function using, and v-model is bind to an input to reterive the data upon submission. Lets submit a for that will take an input and will add the some array. We will also use the v-on or @ to use the event submit and also will be using prevent on it to prevent the regular behaviour of the form.
```
<form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask">
    <button type="submit">Submit</button>
  </form>
```
Here addTask is a function that will run upon submission, and in the v-model we binded the input value to a default value which could be any string or an empty string, for which we have used the variable named newTask in the script.

# Lifecycle Methods
- onBeforeMount = called before mounting begins
- onMounted = called when component is mounted
- onBeforeUpdate = called when reactive data changes and before re-render
- onUpdated = called after re-render
- onBeforeUnmount = called before the Vue instance is destroyed
- OnActivated = called when a kept-alive component is activated
- onDeactivated = called when a kept-alive component is deactivated
- onErrorCaptured = called when an error is caputers from a child component

## onMounted()
To use onMounted you have to import same as ref from vue `import {onMounted} from 'vue'`. We can use this async function or functions inside the onMounted function. Here is the example of fetching an api using it: -
```
onMounted(async () => 
{
  try
  {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  }
  catch(error)
  {
    console.log("Error Fetching Tasks");
  }
});
```