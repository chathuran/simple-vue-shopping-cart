<template>
<div>
  <b-card>
    <b-media no-body>
      <b-media-aside vertical-align="center">
        <b-img  width="72" height="72" alt="placeholder"  v-bind:src="productDetails.image"></b-img>
      </b-media-aside>

      <b-media-body class="ml-3">
        <h5 class="mt-0">{{productDetails.prod_name}}</h5>
        <p>
          {{productDetails.desc}}
        </p>
        <b-media>
        

        <h5 class="mt-0">Price :<strong>{{productDetails.unit_price}}</strong></h5>
         <h5 class="mt-0 text-success" v-if="productDetails.available_unit > 0" ><strong>{{productDetails.available_unit}}</strong> Items Available</h5>
        <h5 class="mt-0 text-danger" v-if="productDetails.available_unit <= 0"><strong>Out of Stocks</strong> </h5>
       
      </b-media>
         
      </b-media-body>
    </b-media>
  </b-card>
</div>



</template>

<script>
export default {
  name: "ProductDetail",
  data() {
    return {
      productDetails: JSON.parse(localStorage.getItem('productDetail'))
    };
  },
  props: {
    
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
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
}
</style>
