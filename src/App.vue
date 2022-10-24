<script >
import axios from 'axios';

export default {
  name: "Beer_App",
  data() {
    return {
      beers: []
    }
  },
  async created() {
    try {
      const res = await axios.get('https://api.punkapi.com/v2/beers');
      this.beers = res.data;
    } catch (error) {
      console.log(error)
    }
  }
  // methods: {
  //   async getData() {
  //     await axios.get('https://api.punkapi.com/v2/beers')
  //       .then(function (response) {
  //         console.log(response)
  //         this.beers = response.data
  //       })
  //       .catch(function (error) {
  //         // handle error
  //         console.log(error);
  //       })
  //       .then(function () {
  //         // always executed
  //       })
  //   }
  // }
}

</script>

<template>
  <p>siema</p>
  <ul>
    <li v-for="beer in beers">
      <p>{{beer.name}}</p>
      <img src={{beer.image_url}} alt="">
    </li>
  </ul>
</template>

<style scoped>

</style>
