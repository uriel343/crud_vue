<template lang="">
  <div>
    <div class="card">
      <div class="card-header">
        <h4>
          Products
          <router-link to="/products/create" class="btn btn-primary"
            >Add Products</router-link
          >
        </h4>
      </div>
    </div>
    <div class="card-body">
      <table class="table table-bordered">
        <thead>
          <tr>
            <th>Name</th>
            <th>Description</th>
            <th>SKU</th>
            <th>Price</th>
          </tr>
        </thead>
        <tbody v-if="this.products.length > 0">
          <tr v-for="(product, index) in this.products" :key="index">
            <td>{{ product.name }}</td>
            <td>{{ product.description }}</td>
            <td>{{ product.sku }}</td>
            <td>{{ product.price }}</td>
            <td>
              <router-link
                :to="{ path: '/products/' + product.id }"
                class="btn btn-success"
                >Update</router-link
              >
              <button
                type="button"
                @click="deleteProduct(product.id)"
                class="btn btn-danger mx-2"
              >
                Delete
              </button>
            </td>
          </tr>
        </tbody>
        <tbody v-else>
          <tr>
            <td colspan="7">Loading ...</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "products",
  data() {
    return {
      products: [],
    };
  },

  mounted() {
    this.getProducts();
  },
  methods: {
    getProducts() {
      axios.get("http://localhost:8000/api/get-all-products").then((res) => {
        this.products = res.data.products;
        console.log(this.products);
      });
    },

    deleteProduct(productId) {
      if (confirm("Are you sure to delete this register?")) {
        axios
          .delete(`http://localhost:8000/api/products/${productId}/delete`)
          .then((res) => {
            alert(res.data.message);
            this.getProducts();
          })
          .catch((error) => {
            alert(error.response.data.message);
          });
      }
    },
  },
};
</script>
<style lang=""></style>
