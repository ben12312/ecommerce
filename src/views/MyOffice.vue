<template>
  <div class="home-component">
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item active" aria-current="page">Barang Saya</li>
        <li class="ml-auto" aria-current="page" style="color: blue;">{{ officeName }}</li>
      </ol>
    </nav>
    <BestProducts></BestProducts>
  </div>
</template>

<script>
// @ is an alias to /src
// BUAT TAMBAH ATAU INSERT PRODUCT

import BestProducts from "@/components/products/BestProducts.vue";
import { getLoggedInUser } from "../components/shared/service/authService";

export default {
  name: "home",
  components: {
    BestProducts,
  },
  data() {
    return {
      newVariable: false,
      buttonNo: true,
      fontsize: 20,
      officeName: ''
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
  created() {
    const loggedUser = getLoggedInUser();
    if (loggedUser) this.officeName = loggedUser.office_name
  }
};
</script>
<style>
.jumbotron {
  padding: 1rem 0rem;
}
</style>
