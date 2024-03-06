<template>
  <div class="cart-products">
    <div class="row mt-5">
      <div class="col-sm-8">
        <form id="productCU">
          <!-- <p v-if="errors.length">
                  <b>Please correct the following error(s):</b>
                  <ul>
                    <li v-for="error in errors" :key="error">{{ error }}</li>
                  </ul>
          </p>-->
          <div class="form-group">
            <label for="productName">Alamat pengambilan barang</label>
            <input
              type="text"
              class="form-control"
              id="productName"
              name="productName"
              aria-describedby="emailHelp"
              placeholder="Alamat pengambilan barang"
            />
          </div>
          <!-- <div class="form-group">
            <label for="productCategory">Address 2</label>
            <input
              type="text"
              class="form-control"
              id="productCategroyDummy"
              placeholder=""
              name="productCategroyDummy"
            />
          </div> -->
          <div class="form-group">
            <label for="productSeller">Waktu pengambilan</label>
            <input
              type="datetime-local"
              class="form-control"
              id="productSellerDummy"
              placeholder="Waktu Pengambilan"
              name="productSellerDummy"
            />
            <label style="font-size: 12px; color: red;">Harap datang sesuai waktu pengambilan</label>
          </div>
          <div class="row">
            <div class="col">
              <div class="form-group">
                <label for="productRating">Status</label>
                <input
                  type="text"
                  class="form-control"
                  id="productRating"
                  placeholder="Status"
                />
              </div>
            </div>
            <div class="col">
              <div class="form-group">
                <label for="productRating">Payment</label>
                <input
                  type="file"
                  class="form-control"
                  id="productRating"
                  placeholder="Status"
                  accept="image/*,.pdf"
                  @change="onFilePicked"
                />
                <label style="font-size: 12px; color: red;">Upload gambar/screen shoot bila diperlukan</label>
              </div>
            </div>
          </div>
          <small id="emailHelp" class="form-text text-muted"
            >Note: Data anda aman dan tidak akan disebarluaskan.</small
          >
          <br />
        </form>
      </div>
      <div class="col-sm-4">
        <cart-calculator ref="cartCalculator"></cart-calculator>
        <ul class="list-group mb-3">
          <router-link to="/products" class="btn btn-primary mt-2 text-white"
            >Continue Shopping</router-link
          >
          <a
            href="javascript:;;"
            class="btn btn-success mt-2 text-white"
            @click="createShippingDetail"
            >Save & Pay</a
          >
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import CartCalculator from "./CartCalculator";
export default {
  name: "Checkout",
  components: { CartCalculator },
  data() {
    return {
      shippingDetail: {
        address1: "",
        address2: "",
        country: "",
        zipCode: "",
        shippingDate: "",
        products: [],
        userId: "",
        totalPrice: "",
      },
      image: null
    };
  },
  methods: {
    createShippingDetail() {},
    onFilePicked (event) {
      const files = event.target.files
      // let filename = files[0].name
      const fileReader = new FileReader()
      fileReader.addEventListener('load', () => {
        this.imageUrl = fileReader.result
      })
      fileReader.readAsDataURL(files[0])
      this.image = files[0]
    }
  },
};
</script>

<style lang="css">
.cart-products > div {
  text-align: start;
}

.cart-products #productCU > div {
  text-align: start;
}

.cart-products #productCU > button {
  text-align: center;
}
</style>
