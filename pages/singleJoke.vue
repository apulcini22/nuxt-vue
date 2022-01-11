<template>
<div>
   <h1>This is the single page dad jokes</h1> 
  <ul>
    <li><nuxt-link to="/">Home</nuxt-link></li>
      <!-- <li>Created At: {{results.icon_url}}</li>
      <li>Id: {{results.id}}</li> -->
      <li>value: {{results.value}}</li>
      <li>id: {{results.id}}</li>
      <li>created_at: {{results.created_at}}</li>
  </ul>
    <section v-if="errored">
    <p>We're sorry, we're not able to retrieve this information at the moment, please try back later</p>
  </section>

  <section v-else>
    <div v-if="loading">Loading...</div>

    <div
      v-else
      v-for="currency in info"
      class="currency"
    >
      {{ currency.description }}:
      <span class="lighten">
        <span v-html="currency.symbol"></span>{{ currency.rate_float | currencydecimal }}
      </span>
    </div>

  </section>
</div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'IndexPage',
  data() {
    return {
      results: null,
      loading: true,
      didError: false,
    }
  },
  async created() {
      const config = {
        headers: {
          Accept: 'application/json',
        }
      }
      try {
      const res = await axios.get('https://api.chucknorris.io/jokes/random', config).then(res => this.results = res.data)
      console.log('res.data::: ', res);
    } 
    catch(error) {
      console.log('error: ', error);
      this.didError = true;
    } 
    finally {
      this.loading = false
    }
    }
  }
</script>
