<template>
<div class="container">
    <div class="row">
        <div class="col-sm-12">
            <table class="table table-hover">
                <thead>
                    <tr>
                        <th>Product</th>
                        <th>Stock</th>
                        <th>Quantity</th>
                        <th class="text-center">Price</th>
                        <th class="text-center">Total</th>
                        <th>Buy</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="product in products" :key="product.id">
                        <td class="col">
                        <div class="media">
                            <a class="thumbnail pull-left" href="#"> <img class="media-object" :src="product.icon" :alt="product.icon" style="width: 72px; height: 72px;"> </a>
                            <div class="media-body">
                                <h4 class="media-heading">{{product.name}}</h4>
                                <h5 class="media-heading"> by {{product.owner}}</h5>
                                <span>Status: </span><span v-bind:class="{'text-success':product.count>0, 'text-danger':product.count===0}"><strong>{{isInStock(product)}}</strong></span>
                            </div>
                        </div></td>
                        <td class="col-sm-1 col-md-1 text-center"><strong>{{product.count}}</strong></td>
                        <td class="col-sm-1 col-md-1" style="text-align: center">
                        <input type="text" class="form-control" v-model="product.desiredQuantity">
                        </td>
                        <td class="col-sm-1 col-md-1 text-center"><strong>{{product.price}}$</strong></td>
                        <td class="col-sm-1 col-md-1 text-center"><strong>{{product.price * product.desiredQuantity}}$</strong></td>
                        <td class="col">
                        <button type="button" class="btn btn-primary">Add</button></td>
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
export default class StorePage extends Vue {
  @Prop() public products: any;

  private isInStock(product: any): String {
    return product.count > 0 ? "In Stock" : "Out of order";
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
