<template>
    <div class="mx-auto">
        <h4>Sliders</h4>
        <div class="sliders">
            <single-slide v-for="img in images" :key="img" :image="img" />
        </div>
    </div>
</template>

<script>
    import SingleSlide from "./SingleSlide";
    export default {
        name: "Sliders",
        components: {
          SingleSlide
        },
        props: {
            images: {
                type: Array
            }
        }
    }
</script>

<style scoped>
    .sliders {
        height: 400px;
        width: 400px;
    }

    .mx-auto {
        margin: 0 auto;
    }
</style>