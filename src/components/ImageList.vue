<template>
    <div class="imageList">
        <Img v-for="(image, index) in images" :key="index" :src="image" :index="index" @remove="remove(index)" />
    </div>
</template>

<script lang="ts">
    import {
        Component,
        Prop,
        Vue,
        Emit
    } from 'vue-property-decorator';
    import Img from './Img.vue';
    @Component({
        components: {
            Img,
        },
    })
    export default class ImageList extends Vue {

        @Prop() private page!: number;
        @Prop() private images!: string[];
        @Prop() private currentIndex!: number;

        remove(index: number) {
            this.$emit('remove', index);
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