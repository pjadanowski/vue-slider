<template>
    <div class="slide-img ">
        <img :src="image" alt="">
<!--        <div class="img" :style="backgroundImg"></div>-->
    </div>
</template>

<script>
    export default {
        name: "SingleSlideModal",
        props: ['image', 'styleProp'],
        data() {
            return {

            }
        },
        methods: {
            closeModal() {

            }
        },
        computed: {
            backgroundImg() {
                return 'background: url(\''+ this.image + ' \') no-repeat center center;'
            }
        }
    }
</script>

<style scoped>
    .slide-img {
        position: relative;
        display: block;
        width: 90%;
        max-width: 1200px;
        height: auto;
        max-height: 90%;
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
    }

    .slide-img:hover {
        cursor: pointer;
    }

    .img {
        -webkit-background-size: cover;
        -moz-background-size: cover;
        -o-background-size: cover;
        background-size: cover;
        width: 90%;
        max-width: 1200px;
        height: auto;
        max-height: 90%;
    }

</style>