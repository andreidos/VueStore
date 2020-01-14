<template>
  <div class="home">
      <div class="row nav-tab">
        <div class="col">
          <a href="" @click.prevent="viewIndex = 0" >Store</a>
        </div>
        <div class="col">
          <a href="" @click.prevent="viewIndex = 1" >Add Item</a>
        </div>
        <div class="col">
          <a href="" @click.prevent="viewIndex = 2" >View Cart ({{cart.length}})</a>
        </div>
    </div>
    <StorePage v-if="viewIndex===0" @addProductToCart="addToCart($event)" @deleteFromCart="removeFromCart($event)" v-bind:products=products v-bind:sessionId=sessionGuid />
    <AddItemPage v-if="viewIndex===1" @childToParent="addProduct($event)" :ownerGuid=sessionGuid />
    <CartPage v-if="viewIndex===2" v-bind:cart=cart :products=products />
  </div>
</template>

<script>
// @ is an alias to /src
import StorePage from "@/components/StorePage.vue";
import AddItemPage from "@/components/AddItemPage.vue";
import CartPage from "@/components/CartPage.vue";

export default {
  name: "home",
  components: {
    StorePage,
    AddItemPage,
    CartPage
  },

data (){
    return {
      viewIndex: 0,
      sessionGuid: this.createGuid(),
      products: [
      {
        id: "1",
        icon: "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
        name: "Some Product",
        owner: "Someone",
        guid: "",
        count: 3,
        price: 4.00,
        desiredQuantity: 0
      },
      {
        id: "2",
        icon: "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
        name: "Some Other Product",
        owner: "Someone Else",
        guid: "",
        count: 1,
        price: 10.99,
        desiredQuantity: 0
      },
      {
        id: "3",
        icon: "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
        name: "Book",
        owner: "Library",
        guid: "",
        count: 10,
        price: 15.00,
        desiredQuantity: 0
      },
      {
        id: "4",
        icon: "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
        name: "Rocks",
        owner: "CaveMan",
        guid: "",
        count: 0,
        price: 1.00,
        desiredQuantity: 0
      }
    ],
    cart: []
    }
  },
  methods: {
    addProduct(product){
      this.viewIndex = 0;
      this.products.push(product);
    },
    addToCart(product){
      let inCart = false;
      for(let i = 0; i < this.cart.length; ++i){
        if(this.cart[i].id === product.id){
          this.cart[i].desiredQuantity += product.desiredQuantity;
          inCart = true;
        }
      }
      if(!inCart){
        this.cart.push(product);
      }
    },
    removeFromCart(product){
      for(let i = 0; i < this.cart.length; ++i){
        if(this.cart[i].id === product.id){
          this.cart.splice(i, 1);
        }
      }
    },
    createGuid(){
      return Math.floor((Math.random()) * 0x10000).toString(16);
    }
  }
};
</script>

<style scoped>
  .nav-tab{
    padding-bottom: 5%;
  }
</style>
