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
                <div class="product-thumbs">
                  <carousel
                    class="product-thumbs-track ps-slider"
                    :items="3"
                    :nav="false"
                    :dots="false"
                  >
                    <div
                      class="pt"
                      @click="changeImage(dataThumb[0])"
                      :class="dataThumb[0] == defaultImg ? 'active' :''"
                    >
                      <img src="img/good-4.png" alt />
                    </div>

                    <div
                      class="pt"
                      @click="changeImage(dataThumb[1])"
                      :class="dataThumb[1] == defaultImg ? 'active' :''"
                    >
                      <img src="img/good-5.png" alt />
                    </div>

                    <div
                      class="pt"
                      @click="changeImage(dataThumb[2])"
                      :class="dataThumb[2] == defaultImg ? 'active' :''"
                    >
                      <img src="img/good-6.png" alt />
                    </div>

                    <div
                      class="pt"
                      @click="changeImage(dataThumb[3])"
                      :class="dataThumb[3] == defaultImg ? 'active' :''"
                    >
                      <img src="img/good-7.png" alt />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details">
                  <div class="pd-title">
                    <span>oranges</span>
                    <h3>Pure Pineapple</h3>
                  </div>
                  <div class="pd-desc">
                    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Corporis, error officia. Rem aperiam laborum voluptatum vel, pariatur modi hic provident eum iure natus quos non a sequi, id accusantium! Autem.</p>
                    <p>
                      Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quam possimus quisquam animi, commodi, nihil voluptate nostrum neque architecto illo officiis doloremque et corrupti cupiditate voluptatibus error illum. Commodi expedita animi nulla aspernatur.
                      Id asperiores blanditiis, omnis repudiandae iste inventore cum, quam sint molestiae accusamus voluptates ex tempora illum sit perspiciatis. Nostrum dolor tenetur amet, illo natus magni veniam quia sit nihil dolores.
                      Commodi ratione distinctio harum voluptatum velit facilis voluptas animi non laudantium, id dolorem atque perferendis enim ducimus? A exercitationem recusandae aliquam quod. Itaque inventore obcaecati, unde quam
                      impedit praesentium veritatis quis beatae ea atque perferendis voluptates velit architecto?
                    </p>
                    <h4>$495.00</h4>
                  </div>
                  <div class="quantity">
                    <router-link to="/cart">
                      <div class="primary-btn pd-cart">Add To Cart</div>
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
// import TeamMember from "../components/TeamMember";
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
      defaultImg: "img/good-4.png",
      dataThumb: [
        "img/good-4.png",
        "img/good-5.png",
        "img/good-6.png",
        "img/good-7.png"
      ]
    };
  },
  methods: {
    changeImage(urlImage) {
      this.defaultImg = urlImage;
    }
  }
};
</script>

<style scoped>
.product-thumbs {
  margin-right: 10px;
}
</style>