<script >
import axios from 'axios';

export default {
  name: "Beer_App",
  data() {
    return {
      beers: [],
      ibuShow: false,
      showBeer: false,
      dispayedBeer: {},
      currentPage: 1,
      filterBeerName: ''
    }
  },
  methods: {
    async fetchData() {
      try {
        const res = await axios.get(`https://api.punkapi.com/v2/beers?page=${this.currentPage}&per_page=20`);
        this.beers = res.data;
      } catch (error) {
        console.log(error)
      }
    },
    displayBeer(beer) {
      this.showBeer = !this.showBeer
      this.dispayedBeer = beer
    }
  },
  mounted() {
    this.fetchData()
  },
  watch: {
    currentPage() {
      this.fetchData()
    }
  },
  computed: {
    filteredBeers() {
      this.beers.filter((beer) => beer.name == this.filterBeerName)
    }
  },
}

</script>

<template >

  <header>
    <h2>Beer Index</h2>
    <div class="action-bar">
      <input type="text" v-model="filterBeerName" placeholder="beer name" />
      <div class="ibu">
        <p>IBU:</p>
        <select name="ibu" id="ibu">
          <option value="5-50">5-50</option>
          <option value="55-100">55-100</option>
          <option value="105-130">105-130</option>
          <option value="all">all</option>
        </select>
      </div>
      <button>SEARCH</button>
      <button>RESET</button>
    </div>
  </header>

  <section class="rendered-beers">
    <ul>
      <li @click="displayBeer(beer)" v-for="beer in beers">
        <h4>{{ beer.name }}</h4>
        <img :src=beer.image_url alt="beer-img">
      </li>
    </ul>
  </section>

  <div class="pagination">
    <ul>
      <li @click="this.currentPage = 1">1</li>
      <li @click="this.currentPage = 2">2</li>
      <li @click="this.currentPage = 3">3</li>
      <li @click="this.currentPage = 4">4</li>
    </ul>
  </div>

  <div v-if="this.showBeer" class="displayed-beer">
    <div class="beer-info">
      <h2>{{ this.dispayedBeer.name }}</h2>
      <p>{{ this.dispayedBeer.description }}</p>
    </div>
    <div class="beer-img">
      <img :src="this.dispayedBeer.image_url" alt="beer_img">
    </div>
    <button @click="this.showBeer = !this.showBeer">X</button>
  </div>

</template>