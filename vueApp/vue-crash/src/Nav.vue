<script setup>
import { ref } from 'vue';

const navs = ref(
{
    home:{
        display: "Home",
        route: "/"
    },
    blog:{
        display: "Blogs",
        route: "/blogs"
    },
    contact:{
        display: "Contact",
        route: "/contact"
    },
});
</script>

<template>
<ul>
    <li v-for="nav in navs" :key="nav"><a :href="nav.route">{{ nav.display }}</a></li>
</ul>
</template>