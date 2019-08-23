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
                <single-slide v-for="(img, index) in slides" :key="index" :image="img" @openLightbox="openLightboxParent"/>
            </div>
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

                document.addEventListener('keyup', function (evt) {
                    if (evt.keyCode === 27) {
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
</style>