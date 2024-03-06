<template>
  <div class="home-component">
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <img alt="Vue logo" src="https://i0.wp.com/pajak.io/wp-content/uploads/2020/10/Strategi-Pajak-Guna-Kelangsungan-Usaha-UKM-UMKM.jpg?w=512&ssl=1" width="200px" />
        <h3 class="display-5 ">
          <span style="color:#42b983">Shoploc </span>
        </h3>
        <p class="lead">Portal pembelian & penjualan untuk UKM/UMKM</p>
      </div>
    </div>
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item active" aria-current="page">Our Best Products</li>
        <li class="ml-auto" aria-current="page"><router-link to="/products">Show All</router-link></li>
      </ol>
    </nav>
    <BestProducts></BestProducts>
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item active " aria-current="page">
          Our Top Products
        </li>
        <li class="ml-auto" aria-current="page">
          <router-link to="/products">Show All</router-link>
        </li>
      </ol>
    </nav>
    <TopProducts></TopProducts>
  </div>
</template>

<script>
// @ is an alias to /src

import BestProducts from "@/components/products/BestProducts.vue";
import TopProducts from "@/components/products/TopProducts.vue";
export default {
  name: "home",
  components: {
    BestProducts,
    TopProducts,
  },
  data() {
    return {
      newVariable: false,
      buttonNo: true,
      fontsize: 20
    };
  },
  methods: {
    yesButton() {
      this.newVariable = true
      this.buttonNo = false
    },
    gedeinButton() {
      this.fontsize = this.fontsize + 3
    },
    noButton() {
      this.buttonNo = false
    }
  },
};
</script>
<style>
.jumbotron {
  padding: 1rem 0rem;
}
</style>
