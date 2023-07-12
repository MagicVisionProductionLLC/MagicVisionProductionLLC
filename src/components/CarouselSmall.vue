<template>
    <div class="carousel">
      <div class="carousel-wrapper" :style="{ transform: `translateX(-${currentSlide * slideWidth}px)` }">
        <div class="carousel-slide" v-for="(item, index) in items" :key="index">
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
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        currentSlide: 0,
        slideWidth: 0,
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
        moveSlide(direction) {
            if (direction === 'next') {
            this.currentSlide++;
            if (this.currentSlide >= this.items.length) {
                this.currentSlide = 0; // Go back to the start
            }
            } else if (direction === 'prev') {
            this.currentSlide--;
            if (this.currentSlide < 0) {
                this.currentSlide = this.items.length - 1; // Go back to the end
            }
            }
        },
        prevSlide() {
            this.moveSlide('prev');
        },
        nextSlide() {
            this.moveSlide('next');
        },
    },
  };
  </script>
  
  <style scoped>
  .carousel {
    position: relative;
    overflow: hidden;
    width: 400px; /* Adjust the width as needed */
    height: 200px; /* Adjust the height as needed */
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
  </style>
  