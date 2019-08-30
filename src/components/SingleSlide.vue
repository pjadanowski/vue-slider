<template>
    <!-- <div class="slide-img"> -->
        <img :src="image" alt="" @click.prevent="openLightbox" class="img-fluid" />
    <!-- </div> -->
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

<style scoped>

    .slide-img {
        position: relative;
        max-height: inherit;
        max-width: inherit;
    }

    img {
        max-height: 100%;
        max-width: 100%;
    }

</style>