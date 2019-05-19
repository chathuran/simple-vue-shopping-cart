<template>
  <div class="hello">
       <b-row>
            <b-col><strong>Products Details</strong></b-col>
            <b-col> <strong> Qty</strong></b-col>
             <b-col><strong> Availability</strong></b-col>
             <b-col><strong> Unit Price </strong></b-col>
              <b-col></b-col>
           </b-row> 
    <div v-bind:key="product_item.id" v-for="product_item in Products">
      <b-list-group>
        <b-list-group-item>
          
          <Product v-bind:product_item="product_item" v-on:updateCart="updateCart($event)"/>
        </b-list-group-item>
      </b-list-group>
    </div>
   
  </div>
  
</template>

<script>
import Product from "./Product.vue";
export default {
  name: "ProductList",
  components: {
    Product
  },
  methods: {
    updateCart: function(prod) {
      this.$emit("updateCart", prod);
    }
  },
  props: ["Products"]
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
</style>
