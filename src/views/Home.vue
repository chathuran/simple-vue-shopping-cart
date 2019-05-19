
<template>
  <div class="home">

    <b-row>
      <b-col cols="8">
        <ProductList v-bind:Products="Products" v-on:updateCart="updateCart($event)"/>
      </b-col>
      <b-col cols="4">
        <Cart
          v-bind:cart="cart"
          v-bind:gross_total="gross_total"
          v-bind:net_total="net_total"
          v-bind:discount="discount"
          v-bind:vat="vat"
          v-on:deleteCartItem="deleteItemfromCart($event)"
        ></Cart>
      </b-col>
    </b-row>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import ProductList from "@/components/ProductList.vue";
import Cart from "@/components/Cart.vue";
export default {
  name: "home",
  components: {
    ProductList,
    Cart
  },
  data() {
    return {
      cart: [],
      net_total: 0,
      gross_total: 0,
      discount: 0,
      vat: 0,
      Products: [
        {
          id: 1,
          image:
            "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
          prod_name: "Product 1",
          desc: " Cras sit amet nibh libero, in gravida nulla. Nulla vel metus scelerisque ante sollicitudin.Cras purus odio, vestibulum in vulputate at, tempus viverra turpis. Fusce condimentum nun ac nisi vulputate fringilla. Donec lacinia congue felis in faucibus",
          unit_price: 300,
          available_unit: 0
        },
        {
          id: 2,
          image:
            "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
          prod_name: "Product 2",
           desc: " Cras sit amet nibh libero, in gravida nulla. Nulla vel metus scelerisque ante sollicitudin.Cras purus odio, vestibulum in vulputate at, tempus viverra turpis. Fusce condimentum nun ac nisi vulputate fringilla. Donec lacinia congue felis in faucibus",
          unit_price: 500,
          available_unit: 7
        },
        {
          id: 3,
          image:
            "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
          prod_name: "Product 3",
           desc: " Cras sit amet nibh libero, in gravida nulla. Nulla vel metus scelerisque ante sollicitudin.Cras purus odio, vestibulum in vulputate at, tempus viverra turpis. Fusce condimentum nun ac nisi vulputate fringilla. Donec lacinia congue felis in faucibus",
          unit_price: 700,
          available_unit: 7
        },
        {
          id: 4,
          image:
            "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
          prod_name: "Product 4",
           desc: " Cras sit amet nibh libero, in gravida nulla. Nulla vel metus scelerisque ante sollicitudin.Cras purus odio, vestibulum in vulputate at, tempus viverra turpis. Fusce condimentum nun ac nisi vulputate fringilla. Donec lacinia congue felis in faucibus",
          unit_price: 1000,
          available_unit: 7
        },
        {
          id: 5,
          image:
            "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
          prod_name: "Product 5",
           desc: " Cras sit amet nibh libero, in gravida nulla. Nulla vel metus scelerisque ante sollicitudin.Cras purus odio, vestibulum in vulputate at, tempus viverra turpis. Fusce condimentum nun ac nisi vulputate fringilla. Donec lacinia congue felis in faucibus",
          unit_price: 1200,
          available_unit: 7
        }
      ]
    };
  },
  methods: {
    updateCart(item) {
      this.gross_total = this.gross_total + item.unit_price * item.selecte_unit;

      // calculate Vat
      this.vat = this.gross_total * 0.12;

      // calculate discount
      if (this.gross_total > 500) {
        this.discount = this.gross_total * 0.02;
      }
      // calculate net-total
      this.net_total = this.gross_total + this.vat - this.discount;
      // this.cart.filter(cartItem => cartItem.id === item.id)
      let itemIndex = this.cart.findIndex(cartItem => cartItem.id === item.id);
      console.log(itemIndex);
      if (itemIndex > -1) {
        this.cart[itemIndex].selecte_unit =
          this.cart[itemIndex].selecte_unit + item.selecte_unit;
      } else {
        this.cart.push(item);
      }
      this.changeAvailabelStackCount(item,"REMOVE");
      console.log(this.cart);
    },
    emptyCart() {
      this.cart = [];
      this.gross_total = 0;
    },

    deleteItemfromCart(item) {
      console.log(item.unit_price);
      this.gross_total = this.gross_total - item.unit_price * item.selecte_unit;

      // calculate Vat
      this.vat = this.gross_total * 0.12;

      // calculate discount
      if (this.gross_total > 500) {
        this.discount = this.gross_total * 0.02;
      }
      // calculate net-total
      this.net_total = this.gross_total + this.vat - this.discount;
      this.cart.splice(item);
      this.changeAvailabelStackCount(item,"ADD");

    },
    changeAvailabelStackCount(item,status) {
      let itemIndex = this.Products.findIndex(
        product => product.id === item.id
      );
      if(status == "REMOVE"){
        this.Products[itemIndex].available_unit =
        this.Products[itemIndex].available_unit - item.selecte_unit;
      }
      if(status == "ADD"){
        this.Products[itemIndex].available_unit =
        this.Products[itemIndex].available_unit + item.selecte_unit;
      }
      
    }
  }
};
</script>
