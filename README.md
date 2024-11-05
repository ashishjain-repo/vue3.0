# Using Vue with CDN

Create a `index.html` file and the script tag from the vuejs.org for CDN place it in your html and then open a script tag and create vue app inside. The vue app contains the method data which returns an object and then we can mount that object to our html with id or class, and can use template script `{{object-key}}` with object key which will return the value of the key pair. We can also create an eveny on something like a button like this `@eventName="methodName"`. To create that method we have to go under the data method in the app and create an object of method and then create a function inside of it. We can also access the objects returned by data using this keyword and access it in the methods.

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

As of latest update one is not required to import defineProps but it is a good practice to import those functionallity.

# Container Component

Container component is a component in which we can wrap some other component, and we can use props on top of it to make it dynamic. We can create a component and pass the tag called `<slot></slot>` where the other component will reside and the main Container is used as a wrapper for that child content or component.

## HomeCards.vue & Card.vue

Card.vue is used here as a Container component which have a div that contains some conent that share parent element which is similar, so we swapped that parent element with Card component, and to make the changes in the parent element we are using props based on the usecase. In this example we are using two blocks or cards who share same parent design but differnet background color, to change that background color we are using Props and we are using Card in the HomeCards to wrap it around some content. Here is the example: -

- Card.vue

```
<script setup>
import { defineProps } from 'vue';

defineProps
(
    {
        bg:{
            type: String,
            default: 'bg-gray-100',
        },
    },
);
</script>

<template>
    <div v-bind:class="`${bg} p-6 rounded-lg shadow-md`">
        <slot>
        </slot>
    </div>
</template>
```

- HomeCards.vue

```
<script setup>
import Card from '@/components/Card.vue';
</script>

<template>
    <section class="py-4">
        <div class="container-xl lg:container m-auto">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4 p-4 rounded-lg">
                <Card>
                    <h2 class="text-2xl font-bold">For Developers</h2>
                    <p class="mt-2 mb-4">
                        Browse our Vue jobs and start your career today
                    </p>
                    <a href="jobs.html" class="inline-block bg-black text-white rounded-lg px-4 py-2 hover:bg-gray-700">
                        Browse Jobs
                    </a>
            </Card>
                <Card bg="bg-green-100">
                    <h2 class="text-2xl font-bold">For Employers</h2>
                    <p class="mt-2 mb-4">
                        List your job to find the perfect developer for the role
                    </p>
                    <a href="add-job.html"
                        class="inline-block bg-green-500 text-white rounded-lg px-4 py-2 hover:bg-green-600">
                        Add Job
                    </a>
                </Card>
            </div>
        </div>
    </section>
</template>
```

In this as we can see instead of passing the class in the quotation marks we uses backticks because when we are binding an attribute we are declaring a variable inside so instead we used backtick to pass the classes, and for the varibale we used `${}` inside the class.

## JobListings.vue & JobListing.vue

On the homepage, we display job listings using a component called JobListings, which pulls job data from a JSON file. It loops through this data and creates a JobListing component for each job. The JobListings component passes job information to JobListing as props. In JobListing, we show details like the job type, title, description, salary, and location, along with a link to read more about each position. Here is the code: -

- JobListings.vue

```
<script setup>
import jobData from '@/jobs2.json';
import JobListing from '@/components/JobListing.vue';

import { ref } from 'vue';

const jobs = ref(jobData);
console.log(jobs);

</script>

<template>
    <section class="bg-blue-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
                Browse Jobs
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListing  v-for="job in jobs" :key="job.id" :job="job"/>
            </div>
        </div>
    </section>

</template>
```

- JobListing.vue

```
<script setup>
import { defineProps } from 'vue';
defineProps
(
    {
        job:Object,
    },
);
</script>

<template>
    <div class="bg-white rounded-xl shadow-md relative">
        <div class="p-4">
            <div class="mb-6">
                <div class="text-gray-600 my-2">{{ job.type }}</div>
                <h3 class="text-xl font-bold">{{ job.title }}</h3>
            </div>

            <div class="mb-5">
                {{ job.description }}
            </div>

            <h3 class="text-green-500 mb-2">{{ job.salary }}</h3>

            <div class="border border-gray-100 mb-5"></div>

            <div class="flex flex-col lg:flex-row justify-between mb-4">
                <div class="text-orange-700 mb-3">
                    <i class="fa-solid fa-location-dot text-lg"></i>
                    {{ job.location }}
                </div>
                <a v-bind:href="'/job/'+job.id"
                    class="h-[36px] bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg text-center text-sm">
                    Read More
                </a>
            </div>
        </div>
    </div>
</template>
```

## JobListings Limit & showButton Props

We created a limit prop which is a number, and when used during declartion we can choose how many jobs are going to be shown. We created a button which will only shown when its props is true otherwise it wont show, for which we using v-if"condition". Here is the code: -

- JobListings.vue

```
<script setup>
import jobData from '@/jobs2.json';
import JobListing from '@/components/JobListing.vue';

import { ref, defineProps } from 'vue';

const jobs = ref(jobData);

defineProps
    (
        {
            limit: Number,
            showButton: {
                type: Boolean,
                default: false,
            },
        },
    );

</script>

<template>
    <section class="bg-blue-50 px-4 py-10">
        <div class="container-xl lg:container m-auto">
            <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
                Browse Jobs
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <JobListing v-for="job in jobs.slice(0, limit || jobs.length)" :key="job.id" :job="job" />
            </div>
        </div>
    </section>
    <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
        <a href="/jobs" class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700">View
            All Jobs</a>
    </section>

</template>
```

- App.vue

```
<script setup>
import Navbar from '@/components/Navbar.vue';
import Hero from '@/components/Hero.vue';
import HomeCards from '@/components/HomeCards.vue';
import JobListings from '@/components/JobListings.vue';
</script>

<template>
  <Navbar />
  <Hero />
  <HomeCards />
  <JobListings :limit="3" :showButton="true"/>
</template>
```

## computed() & Truncate description

Computed is a function that we can use to output something when something depends on something else, which can be a logical expression, or condition. We are using this in our description of jobs, and we are going to bind it to a boolean, if that boolean is false small description or truncated description will show, then we are going to add a button that says more and less based on the boolean variable that we set and toggle the description. Here is the code: -

- JobListing.vue

```
<script setup>
import { defineProps, ref, computed } from 'vue';
const props = defineProps({
    job: Object,
});

const showFullDescription = ref(false);

const toggleFullDescription = () => {
    showFullDescription.value = !showFullDescription.value;
};

const truncatedDescription = computed(() => {
    let description = props.job.description;
    if (!showFullDescription.value) {
        description = description.substring(0, 90) + '...';
    };
    return description;
});
</script>

<template>
    <div class="bg-white rounded-xl shadow-md relative">
        <div class="p-4">
            <div class="mb-6">
                <div class="text-gray-600 my-2">{{ job.type }}</div>
                <h3 class="text-xl font-bold">{{ job.title }}</h3>
            </div>

            <div class="mb-5">
                <div>
                    {{ truncatedDescription }}
                </div>
                <button class="text-green-500 hover:text-green-600 mb-5" @click="toggleFullDescription">{{
                    showFullDescription ? 'Less' : 'More' }}</button>
            </div>

            <h3 class="text-green-500 mb-2">{{ job.salary }}</h3>

            <div class="border border-gray-100 mb-5"></div>

            <div class="flex flex-col lg:flex-row justify-between mb-4">
                <div class="text-orange-700 mb-3">
                    <i class="fa-solid fa-location-dot text-lg"></i>
                    {{ job.location }}
                </div>
                <a v-bind:href="'/job/' + job.id"
                    class="h-[36px] bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg text-center text-sm">
                    Read More
                </a>
            </div>
        </div>
    </div>
</template>
```

## PrimeIcons for adding icons in the Application

To use prime icons we have to install in our application and then import primeicons.css into our main.js file. Here is the command: `npm install primeicons`, import file: `import 'primeicons/primeicons.css'`. Now we can use these icons in the `<i></i>` tags, by defining the classes, you can find more information on that here: [PrimeIcons](https://primevue.org/icons).

# VUE Router

We can install the route when we are creating a new application, but to add the route to an application which does not have router confiured using this command: `npm install vue-router`. Now we can go ahead and create a directory inside the `src` folder named `router`, this is the folder where we are gonna create a file to define router for our application. For this application we are creating a file named `index.js` inside the routes folder where we will be defining the routes for our application. We will be importing two required function from the `vue-router` library called `createRouter` and `createWebHistory`.

# Views

Since we installed Router now to serve the pages on those routes we need views. Views are just pages that containes multiple coponents, and do share some components as well. To create views we are going to start with creating a directory named `views` in `src`, where we are going to create views which we will later serve on those routes using router.

## HomeView.vue

Now we are creating a homevue where only component that are required for homepage will exist, so we are going to move components `Hero`, `HomeCards`, and `JobListings` to that homeview and leave only the navbar, because we require navbar to be on every page. This is the code: -

- HomeView.vue

```
<script setup>
import Hero from '@/components/Hero.vue';
import HomeCards from '@/components/HomeCards.vue';
import JobListings from '@/components/JobListings.vue';
</script>

<template>
    <Hero />
    <HomeCards />
    <JobListings :limit="3" :showButton="true" />
</template>
```

## Create '/' route for HomeView

In the index.js inside the router folder we are also going to import the `HomeView` now. We are going to create a variable which will use the function `createRouter` which takes Object as an argument. We are going to set up history key and add the value of `createWebHistory` function and pass this `import.meta.env.BASE_URL`. We are creating this history so we can use this back and forward in our webpage and it still works as a page that is server rendered. We are also going to define routes key which is an array which takes object as the route, in which we will define: `path`, `name`, and `component`. Now to use this route we have to export default the variable that we created router on. Then we are going to import that in the `main.js` file. Now we are going to make changes and make a variable app and use createApp on that and add `app.use(router)` to add router to the app, and then we are going to mount the app as well. Now for that view to show we are going to import `RouterView` in the `App.vue`, and then we are going to use RouterView as a component after our navbar to show the homeview. Here is the code: -

- router/index.js

```
import {createRouter, createWebHistory} from 'vue-router';

import HomeView from '@/views/HomeView.vue';

const router = createRouter({
    history: createWebHistory(import.meta.env.BASE_URL),
    routes:[
        {
            path:'/',
            name: 'home',
            component: HomeView
        },
    ],
});

export default router;
```

- src/main.js

```
import './assets/main.css';
import 'primeicons/primeicons.css';

import router from './router';

import { createApp } from 'vue'
import App from './App.vue'


const app = createApp(App);

app.use(router);

app.mount('#app');

```

- App.vue

```
<script setup>
import Navbar from '@/components/Navbar.vue';
import { RouterView } from 'vue-router';
</script>

<template>
  <Navbar />
  <RouterView />
</template>
```

## JobsView.vue

Now we are creating `JobsView.vue` file which will contain all the jobs instead of having only 3 as it in HomeView page. This page will return all the jobs available and we are going to set up the router for this.

- JobsView.vue

```
<script setup>
import JobListings from '@/components/JobListings.vue';
</script>

<template>
    <JobListings />
</template>
```

- router/index.js

```
import {createRouter, createWebHistory} from 'vue-router';

import HomeView from '@/views/HomeView.vue';
import JobsView from '@/views/JobsView.vue';

const router = createRouter({
    history: createWebHistory(import.meta.env.BASE_URL),
    routes:[
        {
            path:'/',
            name: 'home',
            component: HomeView
        },
        {
            path:'/jobs',
            name:'jobs',
            component: JobsView
        },
    ],
});

export default router;
```

# RouterLink

Now we are going to replace `<a></a>` to RouterLink, because in vue app, to jump from one route to another we do not rely on anchor tags, instead we use RouterLink and perform functionallity on them. Normal anchor tags do full page reload, but not in RouterLink. URL management is done by Browser using Anchor but with RouterLinkit is managed by RouterLink. This also increased performance in page reaload because a page won't be reloading in SPA, but with anchor tags pages will be doing full reloads. When we are changing the anchor to RouterLink, we also have to change `href` attribute to `to`. So we have changed all the anchor tags to routerlink. Here how it should look like: `<RouterLink to='/route'></RouterLink>`.

## Navbar Active Link

To make our links at the top highlight based on the page we are on we have to first get the path, to get that there is a function that is part of the vue-router called `useRoute`. Now we are going to create a function in navbar using that functions functionallity to receive route and highlight. After setting up that function and using the useRoute attribute called path we can get the path. Now we are going to change the classes based on that route, and to do that we are going to bind the classes. Here is the code:-

- Navbar.vue

```
<script setup>
import logo from '@/assets/img/logo.png'
import { RouterLink, useRoute } from 'vue-router';

const isActiveLink = (routePath) => {
    const route = useRoute();
    return route.path === routePath;
};
</script>

<template>
    <nav class="bg-green-700 border-b border-green-500">
        <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
            <div class="flex h-20 items-center justify-between">
                <div class="flex flex-1 items-center justify-center md:items-stretch md:justify-start">
                    <!-- Logo -->
                    <RouterLink class="flex flex-shrink-0 items-center mr-4" to="/">
                        <img class="h-10 w-auto" v-bind:src="logo" alt="Vue Jobs" />
                        <span class="hidden md:block text-white text-2xl font-bold ml-2">Vue Jobs</span>
                    </RouterLink>
                    <div class="md:ml-auto">
                        <div class="flex space-x-2">
                            <RouterLink to="/"
                                v-bind:class="[isActiveLink('/') ? 'bg-green-900' : 'hover:bg-gray-900', 'hover:text-white', 'text-white', 'px-3', 'py-2', 'rounded-md']">
                                Home</RouterLink>
                            <RouterLink to="/jobs"
                                v-bind:class="[isActiveLink('/jobs') ? 'bg-green-900' : 'hover:bg-gray-900', 'hover:text-white', 'text-white', 'px-3', 'py-2', 'rounded-md']">
                                Jobs</RouterLink>
                            <RouterLink to="/jobs-add"
                                v-bind:class="[isActiveLink('/jobs-add') ? 'bg-green-900' : 'hover:bg-gray-900', 'hover:text-white', 'text-white', 'px-3', 'py-2', 'rounded-md']">
                                Add Job</RouterLink>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </nav>
</template>
```

## NotFound.vue

SO when user is navagating on our wesbsite and get to some page accidentally or added some route that does not exist we are going to show this page. We have created a `NotFound.vue` in our Views and to make that happend we have to create a route and in the path key:value we have to define this: `path:'/:catchAll(.*)',`, it means that it is going to catch all routing errors and show this page or view. Here is the router setup:-

- router/index.js
```
{
    path:'/:catchAll(.*)',
    name:'not-found',
    component: NotFound
},
```
