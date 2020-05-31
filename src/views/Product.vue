<template>
  <div class="poduct">
    <HeaderHome />

    <BreadCrumb />

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
      <div class="container">
        <div class="row">
          <div class="col-lg-12 text-left">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <img class="product-big-img" :src="defaultImg" alt />
                </div>
                <div class="product-thumbs" v-if="productDetails.galleries.length > 0">
                  <carousel
                    class="product-thumbs-track ps-slider"
                    :items="3"
                    :nav="false"
                    :dots="false"
                  >
                    <div
                      v-for="thumb in productDetails.galleries"
                      :key="thumb.id"
                      class="pt"
                      @click="changeImage(thumb.photo)"
                      :class="thumb.photo == defaultImg ? 'active' :''"
                    >
                      <img :src="thumb.photo" alt />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details">
                  <div class="pd-title">
                    <span>{{ productDetails.type }}</span>
                    <h3>{{ productDetails.name }}</h3>
                  </div>
                  <div class="pd-desc">
                    <p v-html="productDetails.description"></p>
                    <h4>${{ productDetails.price }}</h4>
                  </div>
                  <div class="quantity">
                    <router-link to="/cart">
                    <a
                      href="#"
                      class="primary-btn pd-cart"
                      @click="addToCart(productDetails.id, productDetails.name, productDetails.price, productDetails.galleries[0].photo )"
                    >Add To Cart</a>
                    </router-link>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <RelatedProduct />

    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import HeaderHome from "../components/HeaderHome";
import BreadCrumb from "../components/BreadCrumb";
import RelatedProduct from "../components/RelatedProduct";
import axios from "axios";
// import PartnerTeam from "../components/PartnerTeam";
import Footer from "../components/Footer";
import carousel from "vue-owl-carousel";

export default {
  name: "Product",
  components: {
    HeaderHome,
    BreadCrumb,
    carousel,
    RelatedProduct,
    // TeamMember,
    // PartnerTeam,
    Footer
  },
  data() {
    return {
      defaultImg: "",
      productDetails: [],
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
      }

      // check product id
      // productId: this.$route.params.id
    };
  },
  methods: {
    changeImage(urlImage) {
      this.defaultImg = urlImage;
      // check product id
      // console.log(this.productDetails);
    },
    getProductDataAndPicture(data) {
      this.productDetails = data;
      this.defaultImg = data.galleries[0].photo;
    }
  },
  mounted() {
    if (localStorage.getItem("productCart")) {
      try {
        this.productCart = JSON.parse(localStorage.getItem("productCart"));
      } catch (e) {
        localStorage.removeItem("productCart");
      }
    }
    axios
      .get("http://shayna-backend.belajarkoding.com/api/products/", {
        params: {
          id: this.$route.params.id
        }
      })
      .then(res => this.getProductDataAndPicture(res.data.data))
      .catch(err => console.log(err));
  }
};
</script>

<style scoped>
.product-thumbs {
  margin-right: 10px;
}
</style>