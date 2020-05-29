<template>
  <!-- Related Products Section End -->
  <div class="related-products spad">
    <div class="container">
      <div class="row">
        <div class="col-lg-12">
          <div class="section-title">
            <h2>Related Products</h2>
          </div>
        </div>
      </div>
      <div class="row">
        <!-- <carousel
          class="product-slider"
          :items="3"
          :dots="false"
          :loop="true"
          :autoplay="true"
          :nav="false"
        > -->
          <div class="col-lg-3 col-sm-6">
            <div class="product-item">
              <div class="pi-pic">
                <img src="img/good-1.png" alt />
                <ul>
                  <li class="w-icon active">
                    <a href="#">
                      <i class="icon_bag_alt"></i>
                    </a>
                  </li>
                  <li class="quick-view">
                    <a href="#">+ Quick View</a>
                  </li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">Coat</div>
                <a href="#">
                  <h5>Pure Pineapple</h5>
                </a>
                <div class="product-price">
                  $14.00
                  <span>$35.00</span>
                </div>
              </div>
            </div>
          </div>
          <div class="col-lg-3 col-sm-6">
            <div class="product-item">
              <div class="pi-pic">
                <img src="img/good-2.png" alt />
                <ul>
                  <li class="w-icon active">
                    <a href="#">
                      <i class="icon_bag_alt"></i>
                    </a>
                  </li>
                  <li class="quick-view">
                    <a href="#">+ Quick View</a>
                  </li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">Shoes</div>
                <a href="#">
                  <h5>Guangzhou sweater</h5>
                </a>
                <div class="product-price">$13.00</div>
              </div>
            </div>
          </div>
          <div class="col-lg-3 col-sm-6">
            <div class="product-item">
              <div class="pi-pic">
                <img src="img/good-3.png" alt />
                <ul>
                  <li class="w-icon active">
                    <a href="#">
                      <i class="icon_bag_alt"></i>
                    </a>
                  </li>
                  <li class="quick-view">
                    <a href="#">+ Quick View</a>
                  </li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">Towel</div>
                <a href="#">
                  <h5>Pure Pineapple</h5>
                </a>
                <div class="product-price">$34.00</div>
              </div>
            </div>
          </div>
          <div class="col-lg-3 col-sm-6">
            <div class="product-item">
              <div class="pi-pic">
                <img src="img/good-4.png" alt />
                <ul>
                  <li class="w-icon active">
                    <a href="#">
                      <i class="icon_bag_alt"></i>
                    </a>
                  </li>
                  <li class="quick-view">
                    <a href="#">+ Quick View</a>
                  </li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">Towel</div>
                <a href="#">
                  <h5>Converse Shoes</h5>
                </a>
                <div class="product-price">$34.00</div>
              </div>
            </div>
          </div>
        <!-- </carousel> -->
      </div>
    </div>
  </div>
  <!-- Related Products Section End -->
</template>

<script>
// import carousel from "vue-owl-carousel";

export default {
  name: "RelatedProduct",
  components: {
    // carousel
  }
};
</script>

<style>
</style>