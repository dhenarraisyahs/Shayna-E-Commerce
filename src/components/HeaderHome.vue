<template>
  <div class="headerHome">
    <!-- Header Section Begin -->
    <header class="header-section">
      <div class="header-top">
        <div class="container">
          <div class="ht-left">
            <div class="mail-service">
              <i class="fa fa-envelope"></i> hello.shayna@gmail.com
            </div>
            <div class="phone-service">
              <i class="fa fa-phone"></i> +628 22081996
            </div>
          </div>
        </div>
      </div>
      <div class="container">
        <div class="inner-header">
          <div class="row">
            <div class="col-lg-2 col-md-2">
              <div class="logo">
                <a href="./index.html">
                  <img src="img/logo_website_shayna.png" alt />
                </a>
              </div>
            </div>
            <div class="col-lg-7 col-md-7"></div>

            <!-- Shopping Cart -->
            <div class="col-lg-3 text-right col-md-3">
              <ul class="nav-right">
                <li class="cart-icon">
                  Keranjang Belanja &nbsp;
                  <a href="#">
                    <i class="icon_bag_alt"></i>
                    <span>{{productCart.length}}</span>
                  </a>
                  <div class="cart-hover">
                    <div class="select-items">
                      <table v-if="productCart.length > 0">
                        <tbody >
                          <tr v-for="thumbCart in productCart" :key="thumbCart.id">
                            <td class="si-pic">
                              <img :src="thumbCart.photo" alt />
                            </td>
                            <td class="si-text">
                              <div class="product-selected">
                                <p>${{thumbCart.price}} x 1</p>
                                <h6>{{thumbCart.name}}</h6>
                              </div>
                            </td>
                            <td class="si-close">
                              <i class="ti-close" @click="removeProduct(thumbCart.id)"></i>
                            </td>
                          </tr>
                        </tbody>
                      </table>
                      <div v-else>
                        <div class="alert alert-light" role="alert">
                          You didn't choose any products yet!
                          Click
                          <div href="#" class="alert-link">
                            <router-link to="/">Products Highlight,</router-link>
                          </div>to choose your favorite ones!
                        </div>
                      </div>
                    </div>
                    <div class="select-total">
                      <span>total:</span>
                      <h5>${{totalPrice}}.00</h5>
                    </div>
                    <div class="select-button">
                      <router-link to="/cartDetail" class="primary-btn view-card">VIEW CARD</router-link>
                      <a href="#" class="primary-btn checkout-btn">CHECK OUT</a>
                    </div>
                  </div>
                </li>
              </ul>
            </div>
            <!-- Shopping Cart End -->
          </div>
        </div>
      </div>
    </header>
    <!-- Header End -->
  </div>
</template>

<script>
export default {
  name: "HeaderHome",
  data() {
    return {
      productCart: []

      // check product id
      // productId: this.$route.params.id
    };
  },
  methods: {
    removeProduct(idx) {
      //get id for deleted item
      let productCartStorage = JSON.parse(localStorage.getItem("productCart"));
      let itemCartStorage = productCartStorage.map(itemCartStorage => itemCartStorage.id);
      // match id from deleted item and id from storage
      let index = itemCartStorage.findIndex(id => id == idx);
      this.productCart.splice(index, 1);
      //update on localstorage
      const parsed = JSON.stringify(this.productCart);
      localStorage.setItem("productCart", parsed);
      window.location.reload();
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
  },
  computed :{
    totalPrice(){
      return this.productCart.reduce(function(items, data){
        return items + data.price;
      },0);
    }
  }
};
</script>

<style>
.si-pic {
  width: 75px;
}
</style>