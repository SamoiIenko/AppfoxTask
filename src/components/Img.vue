<template>
<div class="showImg">
  <button @click="remove">&times;</button>
  <img :src="src" alt="img">
</div>
</template>

<script lang="ts">
import { Component, Vue, Prop, Emit } from 'vue-property-decorator';

@Component
export default class Img extends Vue {
    @Prop() private src!: string;
    @Prop() private index!: number;


    remove() {
      this.$emit('remove');
    }
}
</script>

<style scoped>

.showImg{
  position: relative;
  width: fit-content;
  margin: 0 auto;
}

button {
  position: absolute;
  border: none;
  border-radius: 50%;
  background-color: #fff;
  font-size: 16px;
  top: 5px;
  right: 5px;
  cursor: pointer;
  transition: .2s;
}
button:hover {
  background-color: #000;
  color: #fff;
}


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
