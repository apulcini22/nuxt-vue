<template>
<div>
   <h1>This is the single page dad jokes</h1> 
  <ul>
    <li><nuxt-link to="/">Home</nuxt-link></li>
    <li><nuxt-link to="/jokeList">Joke List</nuxt-link></li>
  </ul>
    <section v-if="error.didError">
      <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
    </section>

  <section v-else>
    <div v-if="loading">Loading...</div>

    <div v-if="results">
      <br/>
      <hr/>
      <div>Api results below:</div>
      <br/>
      <div>ID: {{results.id}}</div>
      <div>Joke: {{results.joke}}</div>
    </div>
  
  </section>
</div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'SingleJokePage',
  data() {
    return {
      results: null,
      loading: true,
      error: {
        didError: false,
        errorMsg: null
      },
    }
  },
  mounted() {
      const config = {
        headers: {
          Accept: 'application/json',
        }
      }
      const res = axios.get('https://icanhazdadjoke.com/', config)
        .then(res => this.results = res.data)
        .catch(error => {
          console.log('error: ', error);
          this.didError = true;
          this.error.didError = true;
          this.error.errorMsg = error.message;
        })
        .finally(() => this.loading=false);
    }
  }
</script>
