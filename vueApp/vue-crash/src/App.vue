<script>
export default{
  data(){
    return{
      name: 'John Doe',
      status: 'pending',
    };
  },
};
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is Active</p>
  <p v-else-if="status === 'pending'">User is Pending</p>
  <p v-else>User is In-Active</p>
</template>