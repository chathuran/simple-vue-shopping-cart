<template>
  <div class="cart">
    <b-col>
      <h1 class="cart-title">Shopping Cart</h1>
    </b-col>
    <b-row></b-row>
    <b-col v-if="cart.length == 0">
      <p class="cart-empty">Your Shopping Cart is Empty!</p>
    </b-col>

    <b-col v-else>
      <b-list-group>
        <b-row>
          <b-col cols="5"><strong>Product Details</strong></b-col>
          <b-col><strong>Qty</strong></b-col>
          <b-col></b-col>
          <b-col><strong>Total</strong></b-col>
        </b-row>
        <b-col></b-col>


    
         <b-row v-bind:key="item.id" v-for="item in cart">
                <b-col>
                  <b-media right-align vertical-align="center">
                    <img v-bind:src="item.image" class="item-image">
                  </b-media>
                </b-col>
                <b-col>
                  <span class="item-title"><strong>{{item.prod_name}}</strong></span>
                </b-col>
                <b-col>
               
                  <span><strong> x {{item.selecte_unit}}</strong></span>
                </b-col>
                <b-col>
                  <button
                    type="button"
                    class="btn btn-danger btn-block"
                    v-on:click="deleteCartItem($event,item)"
                  >Delete</button>
                </b-col>
                <b-col>
                  <span class="right"> <strong> $ {{item.unit_price * item.selecte_unit}}</strong></span>
                </b-col>
              </b-row>
     
      </b-list-group>
      <b-card>
    
      <b-card-text>
         <b-row>
        <b-col cols="8">
          <span><strong> Total </strong></span>
        </b-col>
        <b-col ></b-col>
        <b-col>
          <span class="right"><strong>$ {{gross_total}}</strong></span>
        </b-col>
      </b-row>
      <b-row>
        <b-col cols="8">
          <span class="left"><strong> Discount</strong></span>
        </b-col>
        <b-col ></b-col>
        <b-col>
          <span class="right"><strong>$ {{discount}}</strong></span>
        </b-col>
      </b-row>
      <b-row>
        <b-col cols="8">
          <span><strong> Vat (12%) </strong></span>
        </b-col>
        <b-col ></b-col>
        <b-col>
          <span class="right pull-right" ><strong>$ {{vat}}</strong></span>
        </b-col>
      </b-row>
      <b-row>
        <b-col cols="8">
          <span><strong> Grand Total </strong></span>
        </b-col>
        <b-col ></b-col>
        <b-col>
          <span class="right"><strong class="left">$ {{net_total}}</strong></span>
        </b-col>
      </b-row>
      </b-card-text>
     
    </b-card>
     
    </b-col>

    <!-- <div class="items" v-else>
      <div class="item clearfix" v-bind:key="item.id"   v-for="item in cart">
        <img v-bind:src="item.image" class="item-image">
        <div class="item-details">
          <p class="item-title">{{item.prod_name}}</p>
          <p class="item-price">
            <span>x{{item.selecte_unit}}</span>
            <span class="right">$ {{item.unit_price * item.selecte_unit}}</span>
          </p>
        </div>
      </div>
    </div>-->
  </div>
</template>

<script>
export default {
  name: "Cart",
  methods: {
    deleteCartItem: function($event, item) {
      this.$emit("deleteCartItem", item);
    }
  },
  props: ["cart", "net_total", "gross_total", "discount", "vat"]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
} */
strong {
    text-align:right
}
</style>
