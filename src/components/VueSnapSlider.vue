<template>
  <div class="slider-wrapper">
    <div class="slider" ref="slider">
      <slot ref="slide"></slot>
    </div>

    <div class="controls" v-if="showControls">
      <slot name="controls">
        <button class="controls__prev" @click="prevSlide">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-chevron-left"
          >
            <polyline points="15 18 9 12 15 6" />
          </svg>
        </button>
        <button class="controls__next" @click="nextSlide">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-chevron-right"
          >
            <polyline points="9 18 15 12 9 6" />
          </svg>
        </button>
      </slot>
    </div>

    <div class="indicator" v-if="showIndicators">
      <button
        class="indicator__button"
        v-for="(slideNumber, index) in numSlides"
        :key="`slide-${index}`"
        @click="scrollTo(index)"
        :class="index === activeSlideIndex ? 'indicator__button--active' : ''"
      >{{ slideNumber }}</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    showControls: {
      type: Boolean,
      default: true
    },
    showIndicators: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      numSlides: 0,
      activeSlideIndex: 0
    };
  },
  methods: {
    setup() {},
    handleScroll() {
      const { scrollLeft, scrollWidth } = this.$refs["slider"];
      const slideWidth = Math.floor(scrollWidth / this.numSlides);
      this.activeSlideIndex = Math.floor(scrollLeft / slideWidth);
    },
    handleResize() {
      let slideWidth;
      if (window.innerWidth > 900) {
        slideWidth = "33.336%";
      } else if (window.innerWidth > 700) {
        slideWidth = "50%";
      } else {
        slideWidth = "100%";
      }

      if (window)
        this.slides.forEach(slide => {
          slide.style.flexBasis = slideWidth;
        });
    },
    nextSlide() {
      this.scrollTo(this.activeSlideIndex + 1);
    },
    prevSlide() {
      this.scrollTo(this.activeSlideIndex - 1);
    },
    scrollTo(index) {
      const scrollLeft = Math.floor(
        this.$refs["slider"].scrollWidth * (index / this.numSlides)
      );
      this.$refs["slider"].scrollTo({
        left: scrollLeft,
        behaviour: "smooth"
      });
    },
    debounce(fn, delay) {
      let timeout;
      return () => {
        clearTimeout(timeout);
        timeout = setTimeout(() => {
          timeout = null;
          fn();
        }, delay);
      };
    }
  },
  mounted() {
    this.handleDebouncedScroll = this.debounce(this.handleScroll, 100);
    this.handleDebouncedResize = this.debounce(this.handleResize, 300);

    this.$refs["slider"].addEventListener("scroll", this.handleDebouncedScroll);
    window.addEventListener("resize", this.handleDebouncedResize);

    // const elementsPerSlide = 2;

    this.numSlides = this.$refs["slider"].children.length;
    this.elementsPerSlide = this.numSlides / 3;
    this.slides = Array.from(this.$refs.slider.children);
  },
  beforeDestroy() {
    this.$refs["slider"].removeEventListener(
      "scroll",
      this.handleDebouncedScroll
    );

    this.$refs["slider"].removeEventListener(
      "resize",
      this.handleDebouncedScroll
    );
  }
};
</script>

<style>
.slider-wrapper {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: calc(50% + 2rem);
}

.slider {
  width: 100%;
  height: 100px;
  display: flex;
  position: relative;

  overflow-x: scroll;
  scroll-behavior: smooth;
  -webkit-overflow-scrolling: touch;
  scroll-snap-type: x mandatory;
  scroll-padding: 0;
  display: flex;
  scrollbar-width: none;
}

.slider::-webkit-scrollbar {
  display: none;
}

.slide {
  /* width: 50%; */
  height: 100%;
  scroll-snap-align: start;
  scroll-snap-stop: normal;
  flex: 33.33334% 0 0;

  display: flex;
  justify-content: center;
  align-items: center;
}

.indicator {
  display: flex;
  margin-top: 1rem;
}

.indicator__button {
  margin: 0 0.25rem;
  width: 1.5rem;
  height: 0.75rem;
  text-indent: -9999999px;
  font-size: 0;
  appearance: none;
  border: none;
  background-color: #e0e0e0;
  outline: none;
  cursor: pointer;
}

.indicator__button--active {
  background-color: #ababab;
}

.controls__prev,
.controls__next {
  appearance: none;
  border: none;

  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  padding: 0;
  top: calc(50% - 1.5rem);
}

.controls__prev {
  left: 0;
}

.controls__next {
  right: 0;
}
</style>
