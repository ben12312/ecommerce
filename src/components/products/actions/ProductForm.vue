<template>
    <div class="productForm">
        <form id="productCU" @submit="actionProduct" v-if="!loading">
          <p v-if="errors.length">
            <b>Please correct the following error(s):</b>
            <ul>
              <li v-for="error in errors" :key="error">{{ error }}</li>
            </ul>
          </p>

          <div class="form-group">
            <label for="productName">Nama Produk</label>
            <input type="text" class="form-control" id="productName" v-model="product.product_name" name="productName" aria-describedby="emailHelp" placeholder="Enter Product Name">
            <small id="emailHelp" class="form-text text-muted">Kami tidak akan mempublikasikan email anda kepihak manapun</small>
          </div>
          <div class="row">
            <div class="col">
              <div class="form-group">
                <label for="isBestProduct">Penjual</label>
                <input type="text" class="form-control" id="isBestProduct" name="isBestProduct" v-model="product.officeName">
              </div>
            </div>
            <div class="col">
              <div class="form-group">
                <label for="productCategory">Kategori Produk</label>
                <select class="form-control" v-if="product.category !== 'Create New'" id="productCategory" name="productCategory" v-model="product.category">
                    <option v-for="(category, index) in categories" :key="index" 
                      v-bind:value="category.productCategory" 
                      >{{category.productCategory}}
                    </option>
                </select>
                <input type="password" class="form-control" id="productCategroyDummy"  v-if="product.category === 'Create New'" placeholder="Password" name="productCategroyDummy" v-model="product.category">
              </div>
            </div>
          </div>

          <!-- <div class="form-group">
            <label for="productSeller">Product Seller</label>
            <select class="form-control"  v-if="product.officeName !== 'Create New'" id="productSeller" name="productSeller" v-model="product.officeName">
                <option 
                  v-for="(seller, index) in sellers" :key="index" 
                  v-bind:value="seller.productSeller" 
                  >{{seller.productSeller}}
                </option>
            </select>
            <input type="password" class="form-control" id="productSellerDummy"  v-if="product.productSeller === 'Create New'" placeholder="Password" name="productSellerDummy" v-model="product.productSellerDummy">
          </div> -->
          <div class="row">
            <div class="col">
              <div class="form-group">
                <label for="isBestProduct">Harga(satuan)</label>
                <input type="text" class="form-control" id="isBestProduct" name="isBestProduct" v-model="product.price" placeholder="Stock">
              </div>
            </div>
            <div class="col">
                <div class="form-group">
                  <label for="isTopProduct">Status</label>
                  <input type="text" class="form-control" id="isTopProduct" name="isTopProduct" placeholder="Password" v-model="product.status">
                </div>
            </div>
            <div class="col">
              <div class="form-group">
                <label for="productRating">Stock</label>
                <input type="number" class="form-control" id="productRating" placeholder="Password" v-model="product.stock">
              </div>
            </div>
          </div>
          <div class="form-group">
            <label for="productImage">Gambar Produk</label>
            <input type="text" class="form-control" id="productImage" v-model="product.picture" placeholder="Product Image URL">
          </div>
          <br>
          <button type="submit" class="btn buttonGreen">Save changes</button>
        </form>

        <div class="lds-dual-ring" v-if="loading"></div>
    </div>
</template>
<script>
import axios from "axios";
import { successToaster } from "../../shared/service/ErrorHandler.js";
// import _ from "lodash";
export default {
  name: "productForm",
  props: ["product"],
  data() {
    return {
      errors: [],
      productCategroyDummy: "",
      productSellerDummy: "",
      categories: [],
      sellers: [],
      loading: false,
    };
  },
  methods: {
    async actionProduct(event) {
      event.preventDefault();
      this.$emit("submit-form", this.product);
      let editData = {}
      editData = this.product
      let resEdit = await axios.put(`${process.env.VUE_APP_BASE_URL}/product/edit`, editData);
      if (resEdit.status == 200) successToaster('success',resEdit.data.messages)
    },
  },
  created() {
    this.categories = [
      {
        id: 1,
        productCategory: "automotive"
      }
    ]
    // this.loading = true;
    // axios.get(`${process.env.VUE_APP_BASE_URL}/products`)
    //   .then((response) => {
    //     // getting all products and getting the uniq value for
    //     // productCategory and returning the productCategory property only
    //     this.categories = _.uniqBy(
    //       _.map(response.data, function (object) {
    //         return _.pick(object, ["productCategory"]);
    //       }),
    //       "productCategory"
    //     );
    //     this.categories.push({ productCategory: "Create New" });

    //     // getting all products and getting the uniq value for
    //     // productSeller and returning the productSeller property only
    //     this.sellers = _.uniqBy(
    //       _.map(response.data, function (object) {
    //         return _.pick(object, ["productSeller"]);
    //       }),
    //       "productSeller"
    //     );

    //     this.sellers.push({ productSeller: "Create New" });

    //     this.loading = false;
    //   })
    //   .catch((error) => {
    //     console.log(error);
    //     errorToaster("Error while fetching products", "");
    //   });
  },
};
</script>
<style lang="css">
.productForm > div {
  text-align: start;
}
.productForm #productCU div {
  text-align: start;
}

.productForm #productCU button {
  text-align: center;
}

.lds-dual-ring {
  display: inline-block;
  width: 64px;
  height: 64px;
}
.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 46px;
  height: 46px;
  margin: 1px;
  border-radius: 50%;
  border: 5px solid #fff;
  border-color: #41b883 transparent #41b883 transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>