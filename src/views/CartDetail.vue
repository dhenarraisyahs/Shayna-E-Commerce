<template>
  <div class="CartDetail">
    <HeaderHome />

    <BreadCrumb />

    <!-- Shopping Cart Section Begin -->
    <section class="shopping-cart spad">
      <div class="container">
        <div class="row">
          <div class="col-lg-8">
            <div class="row">
              <div class="col-lg-12">
                <div class="cart-table">
                  <table>
                    <thead>
                      <tr>
                        <th>Image</th>
                        <th class="p-name text-center">Product Name</th>
                        <th>Price</th>
                        <th>Action</th>
                      </tr>
                    </thead>
                    <tbody v-for="productCarts in productCart" :key="productCarts.id">
                      <tr>
                        <td class="cart-pic first-row">
                          <img :src="productCarts.photo" />
                        </td>
                        <td class="cart-title first-row text-center">
                          <h5>{{productCarts.name}}</h5>
                        </td>
                        <td class="p-price first-row">${{productCarts.price}}</td>
                        <td class="delete-item">
                          <a href="#">
                            <i
                              class="material-icons"
                              @click="removeProduct(productCart.index)"
                            >close</i>
                          </a>
                        </td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
              <div class="col-lg-8">
                <h4 class="mb-4">Informasi Pembeli:</h4>
                <div class="user-checkout">
                  <form>
                    <div class="form-group">
                      <label for="namaLengkap">Nama lengkap</label>
                      <input
                        type="text"
                        class="form-control"
                        id="namaLengkap"
                        aria-describedby="namaHelp"
                        placeholder="Masukan Nama"
                        v-model="customerInfo.name"
                      />
                    </div>
                    <div class="form-group">
                      <label for="namaLengkap">Email Address</label>
                      <input
                        type="email"
                        class="form-control"
                        id="emailAddress"
                        aria-describedby="emailHelp"
                        placeholder="Masukan Email"
                        v-model="customerInfo.email"
                      />
                    </div>
                    <div class="form-group">
                      <label for="namaLengkap">No. HP</label>
                      <input
                        type="text"
                        class="form-control"
                        id="noHP"
                        aria-describedby="noHPHelp"
                        placeholder="Masukan No. HP"
                        v-model="customerInfo.phone"
                      />
                    </div>
                    <div class="form-group">
                      <label for="alamatLengkap">Alamat Lengkap</label>
                      <textarea
                        class="form-control"
                        id="alamatLengkap"
                        rows="3"
                        v-model="customerInfo.address"
                      ></textarea>
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
          <div class="col-lg-4">
            <div class="row">
              <div class="col-lg-12">
                <div class="proceed-checkout">
                  <ul>
                    <li class="subtotal">
                      ID Transaction
                      <span>#SH12000</span>
                    </li>
                    <li class="subtotal mt-3">
                      Subtotal
                      <span>${{$b = totalPrice}}.00</span>
                    </li>
                    <li class="subtotal mt-3">
                      Pajak
                      <span>${{$a = totalPrice * 10 / 100}}.00</span>
                    </li>
                    <li class="subtotal mt-3">
                      Total Biaya
                      <span>${{$b+$a}}.00</span>
                    </li>
                    <li class="subtotal mt-3">
                      Bank Transfer
                      <span>Mandiri</span>
                    </li>
                    <li class="subtotal mt-3">
                      No. Rekening
                      <span>2208 1996 1403</span>
                    </li>
                    <li class="subtotal mt-3">
                      Nama Penerima
                      <span>Shayna</span>
                    </li>
                  </ul>
                  <a @click="checkout()" href="#" class="proceed-btn">I ALREADY PAID</a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Shopping Cart Section End -->
    <Footer />
  </div>
</template>

<script>
import HeaderHome from "../components/HeaderHome";
import BreadCrumb from "../components/BreadCrumb";
import Footer from "../components/Footer";
import axios from "axios";

export default {
  name: "CartDetail",
  components: {
    HeaderHome,
    BreadCrumb,
    Footer
  },
  data() {
    return {
      productCart: [],
      customerInfo: {
        name: "",
        email: "",
        phone: "",
        address: ""
      }

      // check product id
      // productId: this.$route.params.id
    };
  },
  methods: {
    removeProduct(index) {
      this.productCart.splice(index, 1);
      // save shange of product to local storage
      const parsed = JSON.stringify(this.productCart);
      localStorage.setItem("productCart", parsed);
    },
    checkout() {
      // convert all checkout products to be array for trasaction details
      let productIds = this.productCart.map(function(product) {
        return product.id;
      });

      // convert all checkout datas to be object
      let checkoutData = {
        'name': this.customerInfo.name,
        'email': this.customerInfo.email,
        'phone': this.customerInfo.phone,
        'address': this.customerInfo.address,
        "transaction_price": this.totalPrice + (this.totalPrice * 10) / 100,
        "transaction_status": "PENDING",
        "transaction_datils": productIds
      };

      axios
        .post("https://shayna-backend.belajarkoding.com/api/checkout", checkoutData)
        .then(() => this.$router.push('success'))
        .catch(err =>console.log(err));
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
  computed: {
    totalPrice() {
      return this.productCart.reduce(function(items, data) {
        return items + data.price;
      }, 0);
    }
  }
};
</script>

<style>
</style>