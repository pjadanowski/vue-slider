<template>
    <div class="d-flex justify-content-center w-100">
        <h4>Sliders</h4>

        <div class="sliders-wrap">

            <div class="sliders">
                <single-slide v-for="(img, index) in slides" :key="index" :image="img" />
            </div>
            <div class="arrows d-flex justify-content-between align-items-center">
                <div class="left">
                    <button class="btn btn-default" @click.prevent="setCurrentSlide(currentSlide - 1)"> ❮ </button>
                </div>

                <div class="bulets d-flex">
                    <div class="bulet border-ccc mx-1" :class="{'white': index === currentSlide}" v-for="(img, index) in images" :key="index">
                        
                    </div>
                </div>
                <div class="right">
                    <button class="btn btn-default" @click.prevent="setCurrentSlide(currentSlide + 1)"> ❯ </button>
                </div>
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
                slides: this.images
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
            }
        },
        mounted() {
            this.showSlideWithIndex(this.currentSlide)
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
    }
    .arrows button {
        font-size: 3rem;
    }

    .bulet {
        height: 13px;
        width: 13px;
        border-radius: 50%;
        padding: 0;
        background-color: transparent;
    }
    .bulet.white{
        background: #FFF !important;
    }
    .border-ccc {
        border: 1px solid #ccc!important;
    }

</style>