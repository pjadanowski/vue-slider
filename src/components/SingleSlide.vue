<template>
    <div class="slide-img" :style="backgroundImage">
        <h1>asdasd</h1>
    </div>
</template>

<script>
    export default {
        name: "SingleSlide",
        props: ['image'],
        data() {
            return {

            }
        },
        computed: {
            backgroundImage(){
                return {backgroundImage: 'url(\'' + this.image + '\')'}
            }
        }
    }
</script>

<style scoped>
    .slide-img {
        position: relative;
        height: 100%;
        width: 100%;
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
    }
</style>