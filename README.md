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

# Using TailwindCSS with Vue.js
We will be using Postcss autofixer for tailwindcss instead of CLI. This is the command to create the config file for it: `npm install -D tailwindcss@latest postcss@latest autoprefixer@latest`. After running this command we have to create tailwind.config.js and postcss.config.js, but instead we can use this command to do it for use: `npx tailwindcss init -p`. Now we will be configuring the `tailwind.config.js`, in this file in the content array we have to mention which will tailwind should watch for and from which directory. We are going to add the main entry point fist which is `index.html` and then the folder and file extensions that we want to watch `./src/**/*.{vue,js,ts,jsx,tsx}`. We can also made custom adjustment based on the project for this file, since we are doing a project I will be adding some fonts that I would like to use. All those changes will be made in the extend: object in tailwind.config.js. The file would look like this: -
```
/** @type {import('tailwindcss').Config} */
export default {
  content: ['/.index.html', './src/**/*.{vue,js,ts,jsx,tsx}'],
  theme: {
    extend: {
      fontFamily: {
        sans: ['Poppins', 'sans-serif']
      },
      gridTemplateColumns: {
        '70/30': '70% 28%'
      },
    },
  },
  variants: {
    extend: {},
  },
  plugins: [],
}
```
Last thing we have to do to config tailwindcss is to add these following three lines to our CSS file: -
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

# Components and Views
Components are the individual parts that make up a view. A view can consist of multiple components working together to present information and allow user interactions.

## Navbar.vue
We are creating `Navbar.vue` in the components folder because we will be using Navbar in multiple pages. When we are working inside the src folder we can use `import something from '@/assests/'` something like this to import from the src folder instead of using regular paths. So for this component we wrote the template and we imported logo from assets and bind it to the navbar src attribute. After than we simply imported in the App.vue and we used the component with self-closing tag, here is the code: -
- Navbar.vue
```
<script setup>
import logo from '@/assets/img/logo.png'
</script>

<template>
    <nav class="bg-green-700 border-b border-green-500">
        <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
            <div class="flex h-20 items-center justify-between">
                <div class="flex flex-1 items-center justify-center md:items-stretch md:justify-start">
                    <!-- Logo -->
                    <a class="flex flex-shrink-0 items-center mr-4" href="index.html">
                        <img class="h-10 w-auto" v-bind:src="logo" alt="Vue Jobs" />
                        <span class="hidden md:block text-white text-2xl font-bold ml-2">Vue Jobs</span>
                    </a>
                    <div class="md:ml-auto">
                        <div class="flex space-x-2">
                            <a href="index.html"
                                class="text-white bg-green-900 hover:bg-gray-900 hover:text-white rounded-md px-3 py-2">Home</a>
                            <a href="jobs.html"
                                class="text-white hover:bg-green-900 hover:text-white rounded-md px-3 py-2">Jobs</a>
                            <a href="add-job.html"
                                class="text-white hover:bg-green-900 hover:text-white rounded-md px-3 py-2">Add Job</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </nav>
</template>
```
- App.vue
```
<script setup>
import Navbar from '@/components/Navbar.vue';

</script>

<template>
  <Navbar />
</template>
```

## Hero.vue
We created a file `Hero.vue` in components and add the static tags and imported in the App.vue to serve on the main page.

# Props - What are Props?
Props are way to send information to components so they can do their job correctly. When you create a component, you can pass data to it using props. To use props in vue we have to import props in the component which we will be using to pass the data or props in: `import {defineProps} from 'vue'`. We can use this function and we have to pass objects in the function, and then the name of the variable that we would like to use as an attribute and then we have to pass two key value pair inside of it, first what type which could be string, number or other types and then default for when there is no value passed for prop or prop is not used. We can use these multiple variable in a component and their own default behaviours. We use these props when using the component something like this: `<Component propTitle="Some Title" />` if the prop is not used, the default behaviour will show. Here is the example how we are using it in our application: -
- Hero.vue
```
<script setup>
import { defineProps } from 'vue';

defineProps(
    {
        title: {
            type: String,
            default: 'Become a Vue Dev',
        },
        subtitle:{
            type:String,
            default:'Find the Vue job that fits your skills and needs',
        }
    }
)

</script>

<template>
    <section class="bg-green-700 py-20 mb-4">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col items-center">
            <div class="text-center">
                <h1 class="text-4xl font-extrabold text-white sm:text-5xl md:text-6xl">
                    {{title}}
                </h1>
                <p class="my-4 text-xl text-white">
                    {{ subtitle }}
                </p>
            </div>
        </div>
    </section>
</template>
```

- App.vue
```
<script setup>
import Navbar from '@/components/Navbar.vue';
import Hero from '@/components/Hero.vue';
</script>

<template>
  <Navbar />
  <Hero title="Test Title" subtitle="Test Subtitle"/>
</template>
```

