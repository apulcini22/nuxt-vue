<template>
<div>
   <h1>Dad jokes coming your way</h1> 
  <ul>
    <li><nuxt-link to="/singleJoke">Single Joke</nuxt-link></li>
    <li><nuxt-link to="/jokeList">Joke List</nuxt-link></li>
  </ul>
</div>
</template>

<script>
export default {
  name: 'IndexPage',
  }
</script>