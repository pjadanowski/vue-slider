<template>
    <div class="slide-img animate-left">
        <img :src="image" alt="" @click.prevent="openLightbox" class="img-fluid">
    </div>
</template>

<script>
    export default {
        name: "SingleSlide",
        props: ['image', 'styleProp'],
        data() {
            return {
            }
        },
        methods: {
            openLightbox() {
                // console.log("from child");
                this.$emit('openLightbox', this.image)
            },
            closeModal() {

            }
        },
        computed: {
        }
    }
</script>

<style >
    .slide-img {
        position: relative;
        display: block;
        max-height: 100%;
        max-width: 100%;
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
    }

    .slide-img:hover {
        cursor: pointer;
    }


    .animate-left{position:relative;animation:animateleft 0.4s}@keyframes animateleft{from{left:-300px;opacity:0} to{left:0;opacity:1}}



</style>