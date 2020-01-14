<template>
<div class="container">
    <div class="row total-div">
        <b>Total: {{geTotalPrice()}}$</b>
    </div>
    <div class="row">
        <div class="col-sm-12">
            <table class="table table-hover">
                <thead>
                    <tr>
                        <th>Product</th>
                        <th>Quantity</th>
                        <th>Price</th>
                        <th>Total</th>
                        <th>Remove</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="product in cart" :key="product.id">
                        <td class="col">
                        <div class="media">
                            <a class="thumbnail pull-left" href="#"> <img class="media-object" :src="product.icon" style="width: 72px; height: 72px;"> </a>
                            <div class="media-body">
                                <h4 class="media-heading">{{product.name}}</h4>
                                <h5 class="media-heading"> by {{product.owner}}</h5>
                            </div>
                        </div></td>
                        <td class="col-sm-1 col-md-1 text-center"><strong>{{product.desiredQuantity}}</strong></td>
                        <td class="col-sm-1 col-md-1 text-center"><strong>{{product.price}}$</strong></td>
                        <td class="col-sm-1 col-md-1 text-center"><strong>{{product.price * product.desiredQuantity}}$</strong></td>
                        <td class="col">
                        <button type="button" class="btn btn-danger" @click="deleteItem(product)" >X</button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class CartPage extends Vue {
  @Prop() public cart: any;
  @Prop() products: any;

  private deleteItem(product: any): void{
      for(var i = this.cart.length - 1; i >= 0; i--) {
        if(this.cart[i] === product) {
            this.cart.splice(i, 1);
        }
    }
    for(i = this.products.length - 1; i >= 0; i--) {
        if(this.products[i].id === product.id) {
            this.products[i].count = Number(product.desiredQuantity) + Number(this.products[i].count);
        }
    }
  }

  private geTotalPrice(){
      let total = 0;
      for(let i=0; i<this.cart.length; ++i){
          total+=this.cart[i].price * this.cart[i].desiredQuantity;
      }
      return total;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.total-div{
    padding-left: 2%;
}
</style>
