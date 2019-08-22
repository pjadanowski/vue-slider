<template>
    <div>
        <h2>Hello from gallery</h2>

        <sliders :images="images" />
    </div>
</template>

<script>
    import Sliders from "./Sliders";
    export default {
        name: "Gallery",
        components: {Sliders},
        props: ['images'],
        comments: {
            Sliders
        }
    }
</script>

<style scoped>

</style>