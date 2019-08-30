<template>
    <div class="d-flex justify-content-center w-100">
        <div class="sliders-wrap">

            <div class="sliders">
                <single-slide v-for="(img, index) in slides" :key="index" :image="img"
                    @openLightbox="openLightboxParent" />
            </div>
            <div class="arrows d-flex justify-content-between align-items-center">
                <div class="left">
                    <button class="btn btn-default" @click.prevent="setCurrentSlide(currentSlide - 1)"> ❮ </button>
                </div>

                <div class="bulets d-flex">
                    <div class="bulet border-ccc mx-1" :class="{'white': index === currentSlide}"
                        v-for="(img, index) in images" :key="index" @click.prevent="setCurrentSlide(index)"></div>
                </div>
                <div class="right">
                    <button class="btn btn-default" @click.prevent="setCurrentSlide(currentSlide + 1)"> ❯ </button>
                </div>
            </div>
        </div>


        <!-- The Modal/Lightbox -->
        <div class="modal-wrapper" v-if="lightbox" :class="{ 'd-block' : lightbox }">
            <div class="modal-container">

                <div class="modal-header">
                    <div class="btn-wrapper">
                        <button @click.prevent="closeLightbox"> &times; </button>
                    </div>
                </div>

                <div class="modal-body">
                    <div class="img-wrapper">
                        <single-slide-modal v-for="(img, index) in slides" :key="index" :image="img"
                            @openLightbox="openLightboxParent" />
                    </div>
                </div>

                <div class="modal-control position-absolute">
                    <div class="left"> <button class="btn btn-default"
                            @click.prevent="setCurrentSlide(currentSlide - 1)">❮</button> </div>
                    <div class="right"> <button class="btn btn-default"
                            @click.prevent="setCurrentSlide(currentSlide + 1)">❯</button> </div>
                </div>


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
            SingleSlide,
            SingleSlideModal
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
                if (index > this.images.length) {
                    index = 0;
                }
                if (index < 0) {
                    index = this.images.length - 1;
                }

                this.images.forEach((img, ind) => {
                    if (index === ind) {
                        this.slides = [img];
                    }
                })
            },
            showSlide() {
                this.images.forEach((img, ind) => {
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
            },
            listenKeyArrows() {
                let that = this;

                document.addEventListener('keydown', function (evt) {
                    console.log(evt.key);
                    
                    if (evt.key === 'ArrowLeft') { that.setCurrentSlide(that.currentSlide - 1); }
                    if (evt.key === 'ArrowRight') { that.setCurrentSlide(that.currentSlide + 1); }
                });
            }
        },
        mounted() {
            this.showSlideWithIndex(this.currentSlide);

            this.listenForEsc()
            this.listenKeyArrows()
        },
        watch: {
            currentSlide(value) {
                if (this.currentSlide > this.images.length - 1) {
                    this.currentSlide = 0;
                }
                if (this.currentSlide < 0) {
                    this.currentSlide = this.images.length - 1;
                }

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

    .bulet.white {
        background: #FFF !important;
    }

    .border-ccc {
        border: 1px solid #ccc !important;
    }

    .d-block {
        display: block !important;
    }




    .modal-wrapper {
        display: none;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 1043;
        position: fixed;
        outline: none !important;
        background: rgba(0, 0, 0, .85);
    }


    .modal-container {
        text-align: center;
        position: absolute;
        width: 100%;
        height: 100%;
        left: 0;
        top: 0;
        box-sizing: border-box;
    }

    .modal-header {
        position: fixed;
        left: 0;
        top: 0;
        width: 100%;
        height: 40px;
        display: flex;
        justify-content: flex-end;
    }

    .btn-wrapper {
        display: flex;
        align-items: center;
        margin: 0;
        padding: 0;
    }

    .btn-wrapper button {
        background: none;
        outline: none !important;
        border: none !important;
        color: #FFF;
        font-size: 2rem;
        cursor: pointer;
    }


    .modal-body {
        max-height: 100%;
        max-width: 1200px;
        width: 90%;
        height: auto;
        /* border: 1px solid #FFF; */
        margin: 0 auto;
        padding-top: 40px;
    }

    .img-wrapper img {
        position: fixed;
        /* background-color: white; */
        margin: 0;
        padding: 0;
        max-height: 90%;
        max-width: 90%;
        top: 50%;
        left: 50%;
        margin-right: -50%;
        transform: translate(-50%, -50%);
        box-shadow: 0px 0px 12px rgba(0, 0, 0, .8);
    }

    .modal-control {
        color: #FFF !important;
        left: 0;
        top: calc(50% - 1.5rem);
        display: inline-flex;
        justify-content: space-between;
        width: 100vw;
        padding: 0 10px;
        z-index: 999999999;
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