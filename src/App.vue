<template>
  <div>
    <router-link to="/">Home</router-link>
    <router-link to="/users">Users</router-link>
    <router-link to="/about">About us</router-link>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
}
</script>