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
          <a href="" @click.prevent="viewIndex = 2" >View Cart</a>
        </div>
    </div>
    <StorePage v-if="viewIndex===0" v-bind:products=products />
    <AddItemPage v-if="viewIndex===1" @childToParent="addProduct($event)" />
  </div>
</template>

<script>
// @ is an alias to /src
import StorePage from "@/components/StorePage.vue";
import AddItemPage from "@/components/AddItemPage.vue";

export default {
  name: "home",
  components: {
    StorePage,
    AddItemPage
  },

data (){
    return {
      viewIndex: 0,
      products: [
      {
        id: "1",
        icon: "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
        name: "Some Product",
        owner: "Someone",
        count: 3,
        price: 4.00,
        desiredQuantity: 0
      },
      {
        id: "2",
        icon: "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
        name: "Some Other Product",
        owner: "Someone Else",
        count: 1,
        price: 10.99,
        desiredQuantity: 0
      },
      {
        id: "3",
        icon: "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
        name: "Book",
        owner: "Library",
        count: 10,
        price: 15.00,
        desiredQuantity: 0
      },
      {
        id: "4",
        icon: "http://icons.iconarchive.com/icons/custom-icon-design/flatastic-2/72/product-icon.png",
        name: "Rocks",
        owner: "CaveMan",
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
    }
  }
};
</script>

<style scoped>
  .nav-tab{
    padding-bottom: 5%;
  }
</style>
