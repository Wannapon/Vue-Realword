<template>
  <div>
    <section>
      <h2>Total Price: {{ getTotalPrice() }} Baht.</h2>
      <b-button-group>
        <b-btn variant="warning" v-b-toggle.cart>Go to Cart</b-btn>
        <b-btn variant="primary" v-b-toggle.products>Go to Products</b-btn>
      </b-button-group>
    </section>
    <b-collapse accordion="shoppingOne" id="cart" :visible="false">
      <section>
        <b-button-group>
          <b-btn variant="success" :disabled="isEmpty() ? '' : undefined">Purchase All</b-btn>
          <b-btn
            variant="danger"
            :disabled="isEmpty() ? '' : undefined"
            @click="emptyCart"
          >Empty Cart</b-btn>
        </b-button-group>
      </section>
      <section :class="'shopping-cart'">
        <h5 v-if="isEmpty()" class="empty-text">Empty Cart</h5>
        <b-card-group deck :style="{'padding':'15px'}">
          <b-card v-for="(order,index) in cart" :key="index" no-body :class="'fixed-width'">
            <b-card-header>
              <h4>{{order.product.name}}</h4>
            </b-card-header>
            <b-card-img :src="order.product.imgSrc"></b-card-img>
            <b-card-body>
              <p>Quantity: {{order.quantity}}</p>
              <p>Total: {{order.quantity * order.product.price}} Baht</p>
            </b-card-body>
            <b-card-footer>
              <b-btn-group>
                <b-btn
                  variant="danger"
                  @click="removeOneFromCart(order)"
                >Remove One ({{order.quantity}})</b-btn>
                <b-btn variant="danger" @click="removeAllFromCart(order)">Remove All</b-btn>
              </b-btn-group>
            </b-card-footer>
          </b-card>
        </b-card-group>
      </section>
    </b-collapse>
    <b-collapse accordion="shoppingOne" visible id="products">
      <section>
        <b-card-group deck>
          <b-card v-for="(product,index) in products" :key="index" no-body :class="'fixed-width'">
            <b-card-header>
              <h4>{{product.name}}</h4>
            </b-card-header>
            <b-card-img :src="product.imgSrc"></b-card-img>
            <b-card-body>
              <p>{{product.description}}</p>
              <p>Price: {{product.price}} Baht</p>
            </b-card-body>
            <b-card-footer>
              <b-btn variant="primary" @click="addToCart(product)">Add to Cart</b-btn>
            </b-card-footer>
          </b-card>
        </b-card-group>
      </section>
    </b-collapse>
  </div>
</template>
<script>
export default {
  name: "ShoppingCart",
  props: {},
  data() {
    return {
      cart: [],
      products: [
        {
          name: "Halls Mentho-Lyptus Flavor",
          imgSrc: (() => require("@/assets/images/halls.jpg"))(),
          description: "Cool and nice, isn't it?",
          price: 80
        },
        {
          name: "Kitkat Mini",
          imgSrc: (() => require("@/assets/images/kitkat.jpg"))(),
          description: "Snacks with strong chocolate taste even it's smaller.",
          price: 120
        },
        {
          name: "Lay's Original (Family Size)",
          imgSrc: (() => require("@/assets/images/lays.png"))(),
          description: "Bigger for family picnic.",
          price: 40
        }
      ],
      isEmpty() {
        return this.cart.length == 0;
      }
    };
  },
  methods: {
    addToCart(product) {
      let find = this.cart.findIndex(x => x.product == product);
      if (find != -1) {
        this.cart[find].quantity++;
      } else {
        this.cart.push({
          product: product,
          quantity: 1
        });
      }
    },
    emptyCart() {
      this.cart = [];
    },
    removeOneFromCart(order) {
      let find = this.cart.findIndex(x => x == order);
      if (find != -1) {
        if (this.cart[find].quantity == 1) this.cart.splice(find, 1);
        else this.cart[find].quantity--;
      }
    },
    removeAllFromCart(order) {
      let find = this.cart.findIndex(x => x == order);
      if (find != -1) {
        this.cart.splice(find, 1);
      }
    },
    getTotalPrice() {
      let sum = 0;
      this.cart.forEach(order => {
        sum += order.quantity * order.product.price;
      });
      return sum;
    }
  }
};
</script>
<style scoped>
section {
  margin-bottom: 25px;
}
.shopping-cart {
  border: dashed gray 2px;
  border-radius: 5px;
  min-height: 350px;
}
.shopping-cart > .empty-text {
  line-height: 350px;
  user-select: none;
  width: 100%;
  text-align: center;
  padding: 15px;
}
.fixed-width {
  min-width: 300px;
  max-width: 300px;
}
</style>
