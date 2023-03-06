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
          <button type="button" @click="saveProduct" class="btn btn-primary">
            Save
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "productCreate",
  data() {
    return {
      model: {
        product: {
          name: "",
          description: "",
          sku: "",
          price: "",
        },
      },
    };
  },
  methods: {
    saveProduct() {
      axios
        .post("http://localhost:8000/api/create-product", this.model.product)
        .then((res) => {
          console.log(res.data);
          alert(res.data.message);

          this.model.product = {
            name: "",
            description: "",
            sku: "",
            price: "",
          };
        })
        .catch(error => {
            console.log("Error", error.message);
        });
    },
  },
};
</script>
<style lang=""></style>
