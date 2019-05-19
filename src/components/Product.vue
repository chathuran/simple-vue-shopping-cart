<template>
  <div class="product">
    <b-row>
      <b-col>
        <a class="thumbnail pull-left" href="#">
          <img
            class="media-object"
            v-bind:src="product_item.image"
            style="width: 72px; height: 72px;"
          >
        </a>
        <h4 class="media-heading">
         {{product_item.prod_name}}
        </h4>
      
      </b-col>
      <b-col cols="8">
        <b-row>
          <b-col>
            <input
              type="number"
              min="0"
              class="form-control"
              id="unitCount"
              value="3"
              v-model="selectedUnitCount"
            >
          </b-col>
          <b-col>
            <span><strong> / {{product_item.available_unit}}</strong></span>
          </b-col>
          <b-col>
            <strong>{{product_item.unit_price}}</strong>
          </b-col>
        </b-row>
      </b-col>
      <b-col>
        <button
          type="button"
          :disabled="outofStock || product_item.available_unit <= 0 || selectedUnitCount >  product_item.available_unit || selectedUnitCount <= 0"
          class="btn btn-primary btn-block"
          v-on:click="addToCart($event)"
        >Add To Cart</button>
        <button type="button" class="btn btn-info btn-block" v-on:click="vieWProductDetails($event)">View Details</button>
        <span><strong> Status:</strong></span>
        <span v-if="!outofStock && product_item.available_unit > 0 && selectedUnitCount <=  product_item.available_unit " class="text-success">
          <strong> Available</strong>
        </span>
        <span v-if="outofStock || product_item.available_unit <= 0 || selectedUnitCount >  product_item.available_unit" class="text-danger">
          <strong> Out of Stock</strong>
        </span>
      </b-col>
    </b-row>

  </div>
</template>

<script>
export default {
   
  name: "Product",
  props: ["product_item"],
  methods: {
    addToCart: function() {
      console.log(this.product_item.prod_name);
      this.selectedItem = {
        id: this.product_item.id,
        image: this.product_item.image,
        prod_name: this.product_item.prod_name,
        unit_price: this.product_item.unit_price,
        selecte_unit: this.selectedUnitCount
      };
    
      this.$emit("updateCart", this.selectedItem);
    },
    vieWProductDetails:function(){
         localStorage.setItem('productDetail', JSON.stringify(this.product_item));
         this.$router.push('/detail');
    }
  },
  data() {
    return {
      selectedUnitCount: 0,
      selectedItem: {},
      outofStock: false
    };
  },
  watch: {
    selectedUnitCount: function(value) {
      this.selectedUnitCount = parseInt(value);
      if (parseInt(value) > this.product_item.available_unit) {
        this.outofStock = true;
      } else {
        this.outofStock = false;
      }
      console.log(this.selectedUnitCount);
    }
  }
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
