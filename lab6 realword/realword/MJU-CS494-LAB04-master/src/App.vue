<template>
  <div id="app" class="container-fluid">
    <div class="button-row">
      <b-btn v-b-toggle.customchart variant="dark">Customized Chart</b-btn>
      <b-btn v-b-toggle.dragandropimages variant="dark">Image Slide Drag-Drop</b-btn>
      <b-btn v-b-toggle.shoppingcart variant="dark">Shopping Cart</b-btn>
    </div>
    <b-collapse id="customchart" class="mt-2" accordion="onlyOne">
      <b-card>
        <section class="card-body">
          <chart></chart>
        </section>
      </b-card>
    </b-collapse>
    <b-collapse id="dragandropimages" class="mt-2" accordion="onlyOne">
      <b-card>
        <section class="card-body">
          <carousel></carousel>
        </section>
      </b-card>
    </b-collapse>
    <b-collapse id="shoppingcart" class="mt-2" accordion="onlyOne">
      <b-card>
        <section class="card-body">
          <shopping-cart></shopping-cart>
        </section>
      </b-card>
    </b-collapse>
  </div>
</template>

<script>
import Chart from "./components/Chart.vue";
import Carousel from "./components/Carousel.vue";
import ShoppingCart from "./components/ShoppingCart.vue";

export default {
  name: "app",
  components: {
    chart: Chart,
    carousel: Carousel,
    "shopping-cart": ShoppingCart
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin: 60px 0;
}
.button-row .btn {
  margin: 0 5px;
}
</style>
