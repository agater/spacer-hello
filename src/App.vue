<template>
  <div :class="[{ felxStart: step ===1}, 'wrapper']">
    <transition name="slide">
      <img src="./assets/logo.svg"class="logo" v-if="step===1">
    </transition>

    <Claim v-if="step===0" />
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step===1"/>
    <transition name="fade">
      <HeroImage v-if="step===0" />
    </transition>

    <div class="results" v-if="results && !loading && step===1">
      <item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)" />
    </div>

    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>

  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import item from '@/components/item.vue';
import Modal from '@/components/Modal.vue';


const API = 'https://images-api.nasa.gov/search';
// @ is an alias to /src
export default {
  name: 'App',
  components: {
    HeroImage,
    Claim,
    SearchInput,
    item,
    Modal,
  },
  data() {
    return {
      modalOpen:false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: ' ',
      results: [],
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },

    // eslint-disable-next-line
      handleInput: debounce(function()  {
        this.loading = true;
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step =1;
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

  .fade-enter-active, fade-leave-active {
    transition: opacity .3s ease;
  }
  .fade-enter, fade-leave-to {
    transition: opacity 0;
  }

  .slide-enter-active, slide-leave-active {
    transition: margin-top .3s ease;
  }
  .slide-enter, slide-leave-to {
    transition: -50px;
  }

  .wrapper {
    min-height: 100vh;
    position: relative;
    display: flex;
    height: 100vh;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    justify-content: center;

    &.felxStart {
      justify-content: flex-start;
    }
  }

  .logo {
    position: absolute;
    top: 30px;
  }

  .results {
    margin-top: 50px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;

    @media (min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }
</style>

