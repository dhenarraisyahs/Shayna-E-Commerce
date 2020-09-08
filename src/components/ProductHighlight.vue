<template>
  <div class="productHighlight">
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
      <div class="container-fluid">
        <div class="row">
          <div class="col-lg-12 mt-5" v-if="products.length > 0">
            <carousel
              class="product-slider"
              :items="3"
              :dots="false"
              :loop="true"
              :autoplay="true"
              :nav="false"
            >
              <div class="product-item" v-for="product in products" :key="product.id">
                <div class="pi-pic">
                  <img :src="product.galleries[0].photo" alt />
                  <ul>
                    <li
                      class="w-icon active"
                      @click="addToCart(product.id, product.name, product.price, product.galleries[0].photo )"
                    >
                      <router-link to="/" class="primary-btn pd-cart">
                        <i class="icon_bag_alt"></i>
                      </router-link>
                    </li>
                    <li class="quick-view">
                      <router-link :to="'/product/'+product.id">Quick View</router-link>
                    </li>
                  </ul>
                </div>
                <div class="pi-text">
                  <div class="catagory-name">{{ product.type }}</div>
                  <a href="#">
                    <h5>{{ product.name }}</h5>
                  </a>
                  <div class="product-price">
                    ${{ product.price }}
                    <span>$35.00</span>
                  </div>
                </div>
              </div>
            </carousel>
          </div>
          <div class="col-lg-12" v-else>
            <div class="alert alert-danger" role="alert">
              Produk Terbaru tidak ditemukan!
              <a href="#" class="alert-link">Hubungi Admin</a> atau pastikan koneksimu lancar!
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Women Banner Section End -->
  </div>
</template>

<script>
import carousel from "vue-owl-carousel";
import axios from "axios";

export default {
  name: "ProductHighlight",
  components: {
    carousel
  },
  mounted() {
    axios
      .get("http://shayna-backend.belajarkoding.com/api/products")
      .then(res => (this.products = res.data.data.data))
      .catch(err => console.log(err));
      // .catch(console.log('ga bisa'));
    if(localStorage.getItem("productCart")){
      try {
        this.productCart = JSON.parse(localStorage.getItem("productCart"));
      } catch(e) {
        localStorage.removeItem("productCart");
      }
    }
  },
  data() {
    return {
      products: [],
      productCart: [],
      addToCart(productId, productName, productPrice, productPhoto) {
        var productAdded = {
          id: productId,
          name: productName,
          photo: productPhoto,
          price: productPrice
        };
        this.productCart.push(productAdded);

        // save shange of product to local storage
        const parsed = JSON.stringify(this.productCart);
        localStorage.setItem("productCart", parsed);

        window.location.reload();
      }
    };
  }
};
</script>

<style>
.product-item {
  margin-right: 20px;
}

/* .col-lg-12{
    background: red;
} */
</style>