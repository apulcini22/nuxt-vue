<template>
<div>
   <h1>This is the single page dad jokes</h1> 
  <ul>
    <li><nuxt-link to="/">Home</nuxt-link></li>
    <li><nuxt-link to="/singleJoke">Single Joke</nuxt-link></li>
  </ul>
    <section v-if="didError">
      <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
    </section>

  <section v-else>
    <div v-if="loading">Loading...</div>
    <div v-if="jokes.length">
      <hr/>
      <div>Api results below:</div>
      <br/>
      <ol>
        <li v-for="joke in jokes" v-bind:key="joke.id">
          <ul>
            <li>ID: {{joke.id}}</li>
            <li>Joke: {{joke.joke}}</li>
          </ul>
        </li>
      </ol>
    </div> 
  </section>
</div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'listOfJokes',
  data() {
    return {
      jokes: [],
      loading: true,
      didError: false
    }
  },
  mounted() {
      const config = {
        headers: {
          Accept: 'application/json',
        }
      }
      const res = axios.get('https://icanhazdadjoke.com/search', config)
        .then(res => this.jokes = res?.data?.results)
        .catch(error => {
          console.log('error: ', error);
          this.didError = true;
        })
        .finally(() => this.loading=false);
    }
  }
</script>
