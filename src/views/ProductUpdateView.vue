<template lang="">
    <div>
      <div class="card">
        <div class="card-header">Add Products</div>
        <div class="card-body">
          <div class="mb-3">
            <label for="">Name</label>
            <input
              type="text"
              name="name"
              id="name"
              class="form-control"
              v-model="model.product.name"
            />
          </div>
          <div class="mb-3">
            <label for="">Description</label>
            <input
              type="text"
              name="description"
              id="description"
              class="form-control"
              v-model="model.product.description"
            />
          </div>
          <div class="mb-3">
            <label for="">SKU</label>
            <input
              type="text"
              name="sku"
              id="sku"
              class="form-control"
              v-model="model.product.sku"
            />
          </div>
          <div class="mb-3">
            <label for="">Price</label>
            <input
              type="text"
              name="price"
              id="price"
              class="form-control"
              v-model="model.product.price"
            />
          </div>
          <div class="mb-3">
            <button type="button" @click="updateProduct" class="btn btn-primary">
              Update
            </button>
          </div>
        </div>
      </div>
    </div>
  </template>
  <script>
  import axios from "axios";
  
  export default {
    name: "productUpdate",
    data() {
      return {
        model: {
          productId : '',
          product: {
            name: "",
            description: "",
            sku: "",
            price: "",
          },
        },
      };
    },
    mounted(){
        this.productId = this.$route.params.id
        this.getProductData(this.$route.params.id)  
    },
    methods: {
        
      getProductData(productId) {
        axios.get(`http://localhost:8000/api/get-product/${productId}`).then(res => {
            this.model.product.name = res.data.product.name
            this.model.product.description = res.data.product.description
            this.model.product.sku = res.data.product.sku
            this.model.product.price = res.data.product.price
        }).catch(err => {
            if(err.response) {
                if(err.response.status == 404){
                    alert(err.response.data.message)
                }
            }
        });
      },
        
      updateProduct() {
        axios
          .put(`http://localhost:8000/api/products/${this.productId}/update`, this.model.product)
          .then((res) => {
            console.log(res.data);
            alert(res.data.message);     
          })
          .catch(error => {
              alert(error.response.data.message);
          });
      },
    },
  };
  </script>
  <style lang=""></style>
  