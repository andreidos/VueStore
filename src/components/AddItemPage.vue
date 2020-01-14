<template>
<div class="container form-body">
    <div class="row">
        <label>Product Name: </label> <input type="text" class="form-control" v-model="product.name">
    </div>
    <div class="row">
        <label>Owner: </label> <input type="text" class="form-control" v-model="product.owner">
    </div>
    <div class="row">
        <label>Quantity: </label> <input type="text" class="form-control" v-model="product.count">
    </div>
    <div class="row">
        <label>Price: </label> <input type="text" class="form-control" v-model="product.price">
    </div>
    <div class="row">
        <label>Image URL: </label> <input type="text" class="form-control" v-model="product.icon">
    </div>
    <div class="row">
        <div class="btn btn-primary add-btn" v-on:click="emitToParent">Add for sale</div>
    </div>
</div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class AddItemPage extends Vue {
    @Prop() ownerGuid: string;
    product={
         id: "",
         icon: "",
         name: "",
         owner: "",
         guid: "",
         count: undefined,
         price: undefined,
         desiredQuantity: 0
         }
    emitToParent() {
        if(!this.product.name || !this.product.owner || !this.product.count || !this.product.price || isNaN(this.product.count) || isNaN(this.product.price)){
            alert("Please complete all the fields!");
            return;
        }
      this.product.id = this.createGuid() + this.createGuid() + this.createGuid() + this.createGuid();
      this.product.guid = this.ownerGuid;
      this.$emit('childToParent', this.product);
    };
    createGuid(){
      return Math.floor((Math.random()) * 0x10000).toString(16);
    };
    
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.form-body{
    text-align: middle;
    padding-right: 30%;
    padding-left: 30%;
}
.add-btn{
    margin-top: 50px;
}
</style>
