<template>
    <!-- <div class=""> -->
        <img :src="image" >
    <!-- </div> -->
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
            // backgroundImg() {
            //     return 'background: url(\''+ this.image + ' \') no-repeat center center;'
            // }
        }
    }
</script>

<style scoped>
    

</style>