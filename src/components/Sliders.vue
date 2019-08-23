<template>
    <div class="d-flex justify-content-center w-100">
        <div class="sliders-wrap">

            <div class="sliders">
                <single-slide v-for="(img, index) in slides" :key="index" :image="img" @openLightbox="openLightboxParent"/>
            </div>
            <div class="arrows d-flex justify-content-between align-items-center">
                <div class="left">
                    <button class="btn btn-default" @click.prevent="setCurrentSlide(currentSlide - 1)"> ❮ </button>
                </div>

                <div class="bulets d-flex">
                    <div class="bulet border-ccc mx-1" :class="{'white': index === currentSlide}" 
                         v-for="(img, index) in images" :key="index"
                         @click.prevent="setCurrentSlide(index)"
                    ></div>
                </div>
                <div class="right">
                    <button class="btn btn-default" @click.prevent="setCurrentSlide(currentSlide + 1)"> ❯ </button>
                </div>
            </div>
        </div>


        <!-- The Modal/Lightbox -->
        <div id="myModal" class="modal" v-if="lightbox" :class="{ 'd-block' : lightbox }" @keyup.esc="closeLightbox">
            <span class="close cursor" @click.prevent="closeLightbox">&times;</span>
            <div class="modal-content">
                <single-slide-modal v-for="(img, index) in slides" :key="index" :image="img" @openLightbox="openLightboxParent"/>
            </div>

            <div class="modal-control position-absolute">
                <div class="left"> <button class="btn btn-default" @click.prevent="setCurrentSlide(currentSlide - 1)">❮</button> </div>
                <div class="right">  <button class="btn btn-default" @click.prevent="setCurrentSlide(currentSlide + 1)">❯</button> </div>
            </div>
        </div>
    </div>
</template>

<script>
    import SingleSlide from "./SingleSlide";
    import SingleSlideModal from "./SingleSlideModal";
    
    export default {
        name: "Sliders",
        components: {
          SingleSlide, SingleSlideModal
        },
        data() {
            return {
                currentSlide: 0,
                slides: this.images,
                lightbox: false
            }
        },
        props: {
            images: {
                type: Array
            }
        },
        methods: {
            showSlideWithIndex(index) {
                if (index > this.images.length) { index = 0; }
                if (index < 0) { index = this.images.length - 1 ; }

                this.images.forEach( (img, ind ) => {
                    if (index === ind) {
                        this.slides = [img]; 
                    }
                })
            },
            showSlide() {
                this.images.forEach( (img, ind ) => {
                    if (this.currentSlide === ind) {
                        this.slides = [img]; 
                    }
                })
            },
            setCurrentSlide(numb) {
                this.currentSlide = numb;
            },
            openLightboxParent() {
                console.log("modal parent");
                this.lightbox = true;
                
            },
            closeLightbox() {
                console.log("closing");
                this.lightbox = false;
            },
            listenForEsc() {
                let that = this;

                document.addEventListener('keydown', function (evt) {
                    if (evt.key === 'Escape' && that.lightbox) {
                        that.closeLightbox();
                    }
                });
            }
        },
        mounted() {
            this.showSlideWithIndex(this.currentSlide);

            this.listenForEsc()
        },
        watch: {
            currentSlide(value) {
                if (this.currentSlide > this.images.length - 1) { this.currentSlide = 0; }
                if (this.currentSlide < 0) { this.currentSlide = this.images.length - 1 ; }

                this.showSlideWithIndex(this.currentSlide)
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

    .arrows {
        display: flex;
        /* position: absolute; */
        /* top:50%; */
        z-index: 99999999999999999;
        background: #f0f0f0;
    }
    .arrows button {
        font-size: 3rem;
    }
    .arrows button:focus,
    .arrows button:active {
        outline: 0;
        box-shadow: none;
    }

    .bulet {
        height: 13px;
        width: 13px;
        border-radius: 50%;
        padding: 0;
        background-color: transparent;
        cursor: pointer;
    }
    
    .bulet.white{
        background: #FFF !important;
    }
    .border-ccc {
        border: 1px solid #ccc!important;
    }

    .d-block {
        display: block !important;
    }










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
        background: none;
        margin: auto;
        padding: 0;
        width: 90%;
        max-width: 1200px;
        height: auto;
        max-height: 90%;
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

    .modal-control {
        color: #FFF !important;
        left: 0;
        top: calc(50% - 1.5rem);
        display: inline-flex;
        justify-content: space-between;
        width: 100vw;
        padding: 0 10px;
        z-index: 99999999999999999999999999999;
    }
    .modal-control button {
        color: #FFF !important;
        margin: 0 !important;
        padding: 0 !important;
        font-size: 3rem;
        border: 1px solid #ccc;
        border-radius: 50%;
        width: 4.5rem !important;
        height: 4.5rem !important;
    }

    .modal-control .right {
        right: 0 !important;
    }
</style>