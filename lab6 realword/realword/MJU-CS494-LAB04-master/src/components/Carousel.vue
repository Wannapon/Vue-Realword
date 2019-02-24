<template>
  <div>
    <div class="image-set">
      <img
        draggable="true"
        src="@/assets/images/096df0eb195b8f0d9475924f9a1e9425.jpg"
        @dragstart="prepareInsertion"
      >
      <img draggable="true" src="@/assets/images/174761.jpg" @dragstart="prepareInsertion">
      <img
        draggable="true"
        src="@/assets/images/Rainfall-Girl-Anime-Live-Wallpaper-Free-1.jpg"
        @dragstart="prepareInsertion"
      >
      <img draggable="true" src="@/assets/images/VQaJKNO.png" @dragstart="prepareInsertion">
    </div>
    <div @dragover="preventDragDropSideEffect" @drop="insertCarouselSlide">
      <b-carousel
        id="dragdrop"
        style="text-shadow: 1px 1px 2px #333; min-height: 50vh;"
        controls
        indicators
        background="#ababab"
        :interval="0"
        img-width="100vw"
        img-height="50vh"
        v-model="slide"
        @sliding-start="onSlideStart"
        @sliding-end="onSlideEnd"
      >
        <b-carousel-slide
          v-for="(src,index) in image_sources"
          v-bind:key="index"
          v-bind:img-src="src"
          draggable="false"
        ></b-carousel-slide>
        <b-carousel-slide img-blank v-if="image_sources.length == 0"></b-carousel-slide>
      </b-carousel>
    </div>

    <!-- <p class="mt-4">
      Slide #: {{ slide }}
      <br>
      Sliding: {{ sliding }}
    </p>-->
  </div>
</template>
<script>
export default {
  name: "Carousel",
  props: {},
  data() {
    return {
      slide: 0,
      image_sources: [],
    };
  },
  methods: {
    onSlideStart(index) {
      // console.log(index)
    },
    onSlideEnd(index) {
      // console.log(index)
    },
    prepareInsertion(ev) {
      ev.dataTransfer.setData("img-src", ev.srcElement.src);
    },
    preventDragDropSideEffect(ev) {
      ev.preventDefault();
    },
    insertCarouselSlide(ev) {
      ev.preventDefault();
      this.image_sources.push(ev.dataTransfer.getData("img-src"));
      for(let i = 0; i < this.image_sources.length; i++){
          this.image_sources[i] == '' ? this.image_sources.splice(i,1) : void(0);
      }
      setTimeout(() => (this.slide = this.image_sources.length - 1), 0);
    }
  }
};
</script>
<style scoped>
.image-set {
  background-color: black;
}
.image-set > img {
  width: 25%;
  display: inline-block;
}
</style>
