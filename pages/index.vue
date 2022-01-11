<template>
<div>
   <h1>Dad jokes coming your way</h1> 
  <ul>
    <li><nuxt-link to="/singleJoke">Single Joke</nuxt-link></li>
    <li>list of jokes</li>
    <li>{{results.results[0]}}</li>
  </ul>
</div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'IndexPage',
  data() {
    return {
      results: null
    }
  },
  async created() {
      const config = {
        headers: {
          Accept: 'application/json',
        }
      }
      try {
      const res = await axios.get('https://icanhazdadjoke.com/search', config).then(res => this.results = res.data)
      console.log('res.data::: ', res);
    } 
    catch(error) {
      console.log('error: ', error);
    }
    return {hello: "hi"}
    }
  }
</script>