<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{ piven }}</h1>
    <h1>{{ sobaqa }}</h1>
    <h1>{{ Pivaqa }}</h1>
    <h1>{{ counter }}</h1>
    <button @click="incrementCounter"></button>
    
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
  piven = "Qqareq";
  sobaqa = "Gau";
  counter = 0;

  get Pivaqa () {
    return this.piven + ' ' + this.sobaqa;
  }

  incrementCounter() {
    this.counter++;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
