<template>
  <div class="cardTemplate">
    <div class="card mb-4 shadow-sm">
      <img
        class="card-img-top mt-2"
        v-bind:src="item.picture"
        alt="Card image cap"
        style="max-height: 320px; max-width: 230px; margin: auto"
      />
      <div class="card-body">
        <h6 class="card-text">{{ item.product_name }}</h6>
        <hr style="margin-top: -50px;">
        <p style="text-align: justify; font-size: 12px; color: grey; margin-top: -10px;">
          <strong>Kategori: {{ item.category }}</strong>
        </p>
        <p style="text-align: justify; font-size: small; margin-top: -12px;" class="card-text"
          ><strong>Deskripsi: </strong>
          {{ (item.description && item.description.length > 53) ? `${item.description.slice(0,53)}...` : item.description }}
        </p>

        <div class="d-flex justify-content-between align-items-center" style="position: absolute; bottom: 0;">
          <div class="btn-group" style="margin-bottom: 10px;">
            <button
              type="button"
              class="btn btn-sm btn-outline-secondary"
              v-on:click="navigateProductDetail(item)"
            >View</button>
            <!-- v-if="loggedUser && loggedUser.isAdmin" -->
            <button
              type="button"
              class="btn btn-sm btn-outline-secondary"
              v-on:click="updateEditProduct(item, item.id)"
            >Edit</button>
          </div>
          <small class="text-muted footerIcons" style="margin-bottom: 10px; margin-left: 75px;">
            <a href="javascript:;;" class="p-2">
              <i class="fa fa-heart"></i>
            </a>
            <a href="javascript:;;" class="p-2" v-on:click="addToCart(item)">
              <i class="fa fa-shopping-cart"></i>
            </a>
          </small>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState, mapMutations } from "vuex";
import { infoToaster, successToaster } from "./service/ErrorHandler";

import _ from "lodash";
export default {
  name: "cardTemplate",
  props: ["item"],
  data() {
    return {
      showModal: false,
    };
  },
  components: {},
  computed: mapState(["loggedUser"]),
  methods: {
    navigateProductDetail(product) {
      this.$router.push({
        name: "productDetails",
        params: { id: product.id },
      });
    },

    ...mapMutations(["ADD_CART_LOCAL"]),

    addToCart(product) {
      const data = _.find(this.$store.getters.cartProducts, product);
      if (data) {
        infoToaster("Already Added", "Product Already Added");
      } else {
        successToaster("Added Successfully", "Product Added Successfully");
        this.ADD_CART_LOCAL(product);
      }
    },

    // this will trigger the parentComponent function
    updateEditProduct(product, id) {
      console.log(id);
      this.$parent.editProduct(product);
    },
  },
  mounted() {},
};
</script>
