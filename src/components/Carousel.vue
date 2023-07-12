<template>
    <div class="carousel">
      <div class="carousel-wrapper" :style="{ transform: `translateX(-${currentSlide * slideWidth}px)` }">
        <div class="carousel-slide" v-for="(item, index) in items" :key="index" @click="openImage(item.imageUrl)">
          <img :src="item.imageUrl" :alt="item.altText">
        </div>
      </div>
      <div class="carousel-controls">
        <button class="carousel-button prev" @click="prevSlide">
          <i class="fas fa-chevron-left"></i>
        </button>
        <button class="carousel-button next" @click="nextSlide">
          <i class="fas fa-chevron-right"></i>
        </button>
      </div>
      <div class="image-popup" v-if="showPopup" @click="closeImage">
        <img :src="clickedImageUrl" :alt="clickedImageAlt">
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        currentSlide: 0,
        slideWidth: 0,
        showPopup: false,
        clickedImageUrl: '',
        clickedImageAlt: ''
      };
    },
    props: {
      items: {
        type: Array,
        required: true,
      },
    },
    mounted() {
      this.slideWidth = this.$el.offsetWidth;
    },
    methods: {
      prevSlide() {
        if (this.currentSlide > 0) {
          this.currentSlide--;
        }
      },
      nextSlide() {
        if (this.currentSlide < this.items.length - 1) {
          this.currentSlide++;
        }
      },
      openImage(imageUrl) {
        this.clickedImageUrl = imageUrl;
        this.clickedImageAlt = this.items.find(item => item.imageUrl === imageUrl).altText;
        this.showPopup = true;
      },
      closeImage() {
        this.showPopup = false;
      }
    },
  };
  </script>
  
  <style scoped>
  .carousel {
    position: relative;
    overflow: hidden;
    width: 1000px; /* Adjust the width as needed */
    height: 500px; /* Adjust the height as needed */
  }
  
  .carousel-wrapper {
    display: flex;
    transition: transform 0.3s ease;
  }
  
  .carousel-slide {
    flex: 0 0 100%;
  }
  
  .carousel-slide img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  
  .carousel-controls {
    position: absolute;
    top: 50%;
    left: 0;
    right: 0;
    display: flex;
    justify-content: space-between;
    transform: translateY(-50%);
  }
  
  .carousel-button {
    background: transparent;
    border: none;
    padding: 5px;
    color: #fff; /* Adjust the button color as needed */
    font-size: 16px; /* Adjust the button font size as needed */
    cursor: pointer;
  }
  
  .carousel-button i {
    pointer-events: none;
  }
  
  .image-popup {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.8);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 9999;
    cursor: pointer;
  }
  
  .image-popup img {
    max-width: 90%;
    max-height: 90%;
    object-fit: contain;
  }
  
  </style>
  