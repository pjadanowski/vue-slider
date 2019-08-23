<template>
    <div class="slide-img animate-left">
        <img :src="image" alt="" class="img-fluid" @click.prevent="openLightbox">
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
        height: 100%;
        width: 100%;
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
    }

    .slide-img:hover {
        cursor: pointer;
    }

    
    .animate-left{position:relative;animation:animateleft 0.4s}@keyframes animateleft{from{left:-300px;opacity:0} to{left:0;opacity:1}}



    /* The Modal (background) */
    .modal {
        display: none;
        position: fixed;
        z-index: 1;
        padding-top: 100px;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        overflow: auto;
        background-color: rgba(0, 0, 0, .8);
    }

    /* Modal Content */
    .modal-content {
        position: relative;
        background-color: #fefefe;
        margin: auto;
        padding: 0;
        width: 90%;
        max-width: 1200px;
    }

    /* The Close Button */
    .close {
        color: white;
        position: absolute;
        top: 10px;
        right: 25px;
        font-size: 35px;
        font-weight: bold;
        z-index: 100;
    }

    .close:hover,
    .close:focus {
        color: #999;
        text-decoration: none;
        cursor: pointer;
    }
</style>