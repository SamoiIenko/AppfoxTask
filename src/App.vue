<template>
  <div id="app">
    <ImageList :images="currentPageImages" @remove="remove"/>
    <div class="buttonGroup">
      <button @click="Prev">Prev</button>
      <button @click="Next">Next</button>
    </div>
  </div>
</template>

<script lang="ts">
  import { Component, Vue } from 'vue-property-decorator';
  import ImageList from './components/ImageList.vue';
  import axios from 'axios';

  @Component({
    components: {
      ImageList,
    },
  })

  export default class App extends Vue {

    pageNumber: number;
    pageStep: number;
    images: string[] = [];
    currentPageImages: string[] = [];
    currentIndex: number;

    constructor() {
      super();
      this.pageNumber = 0;
      this.pageStep = 10;
      this.currentIndex = 0;
    }

    mounted() {
      axios({
          method: 'GET',
          url: 'https://api.unsplash.com/photos/random/?client_id=seC9CrEl86e-z-hrpUKWWcx3z79VSTLGgr3DuswNZ5s&count=30',
        })
        .then((response: any) => {

          for (const image of response.data) {
            this.images.push(image.urls.small);
          }
        })
        .then(() => {
          this.currentPageImages = this.images.slice(0, this.pageStep);
        });
    }

    Prev() { 
       if(this.pageNumber > 0) {
          this.pageNumber--;
          this.currentPageImages = this.images.slice(this.pageNumber*this.pageStep, (this.pageNumber+1)*this.pageStep);
          window.scrollTo(0,0);
       }
    }

    Next() {
      if(this.pageNumber <= this.pageCount) {
          this.pageNumber++;
          this.currentPageImages = this.images.slice(this.pageNumber*this.pageStep, (this.pageNumber+1)*this.pageStep);
          window.scrollTo(0,0);
      }
    }

    get pageCount(): number {
     return Math.round(this.currentPageImages.length / this.pageStep);
    }

    removeImage(index: number) {
      this.images.splice(index, 1);
    }

    remove(index: number) {
     console.log(index);
     this.images.splice(index, 1);
    this.currentPageImages = this.images.slice(this.pageNumber*this.pageStep, (this.pageNumber+1)*this.pageStep);
    }

  }
</script>

<style scoped>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  button {
    background-color: chocolate;
    border: 1px solid #000;
    border-radius: 10px;
    font-size: 15px;
    color: #fff;
    transition: .2s;
    margin-right: 20px;
    text-transform: uppercase;
    padding: 5px 10px;
    cursor: pointer;
  }

  button:hover {
    background-color: coral;
  }
</style>