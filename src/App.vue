<template>
  <div class="wrapper">
    <Claim />
    <SearchInput v-model="searchValue" @input="handleInput"/>
    <HeroImage/>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';


const API = 'https://images-api.nasa.gov/search';
// @ is an alias to /src
export default {
  name: 'App',
  components: {
    HeroImage,
    Claim,
    SearchInput,
  },
  data() {
    return {
      searchValue: ' ',
      results: [],
    };
  },
  methods: {
    // eslint-disable-next-line
      handleInput: debounce(function()  {
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>


<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');

  $font-weight-light: 300;
  $font-weight-normal: 400;
  $font-weight-bold: 600;
  $font-weight-black: 800;

  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  body {
    font-family: 'Monserrat', sans-serif;
    margin: 0;
    padding: 0;
  }

  .wrapper {
    min-height: 100vh;
    display: flex;
    height: 100vh;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    justify-content: center;

  }
</style>

