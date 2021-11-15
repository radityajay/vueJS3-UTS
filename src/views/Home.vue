<script>
import items from '../data/items'
import ProductDisplay from '../components/ProductDisplay.vue'
import ProductPopUp from '../components/ProductPopUp.vue'
import CustTable from '../components/CustTable.vue'
import FormCust from '../components/FormCust.vue'
import FooterDisplay from '../components/FooterDisplay.vue'


export default{
    name: 'Home',
    components: {
    ProductDisplay,
    ProductPopUp,
    CustTable,
    FormCust,
    FooterDisplay
},
    data(){
        return {
          cart: 0,
          items: items,
          product: null,
          active: {
              product_popUp: false
          },
          reviews: [],
          customers: [
                {
                    id: 1,
                    name: 'Bambang',
                    kode: 80119,
                    alamat: 'Jl.Kenanga',
                },
                {
                    id: 2,
                    name: 'Dika',
                    kode: 80351,
                    alamat: 'Jl.Mangga',
                },
                {
                    id: 3,
                    name: 'Agus',
                    kode: 80361,
                    alamat: 'Jl.Mataram',
                },
            ],
        }
    },
    methods:{
        addCart(){
            this.cart += 1
        },
        delCart(){
            if(this.cart != 0){
                this.cart -= 1
            }
        },
        viewProduct(product){
            this.product = product
            this.active.product_popUp = true
            console.log(this.product)
        },
        closeProductPopUs(){
            this.active.product_popUp = false
        },
        addAddress(customer){
            this.customers.push(customer)
        },
        editAddress(id,data){
          this.customers = this.customers.map(function (customer) { 
            return customer.id === id ? data : customer;
          });
        },
        deleteAddress(id){
          this.customers = this.customers.filter(function (customer) { 
            return customer.id !== id;
          });
        }
    }
}
</script>
<template>
  <!-- navbar -->
  <nav class="navbar navbar-expand-lg navbar-light shadow-lg fixed-top" style="background-color: rgba(250, 250, 250, 0.7) !important;">
        <div class="container">
          <a class="navbar-brand" href="#">
            <img src="../assets/images/layerLogo1.png" alt="logos" width="50" height="50">
          </a>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarText" aria-controls="navbarText" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse text-right" id="navbarText">
            <ul class="navbar-nav ms-auto mb-2 mb-lg-0 fw-bold">
              <li class="nav-item">
                <select class="form-select" aria-label="Default select example">
                  <option disabled selected>Location</option>
                  <option v-for="customer in customers" :key="customer.id" value="1">
                    {{customer.alamat}}
                    </option>
                </select>
              </li>
              <li class="nav-item fw-medium">
                <a class="nav-link " href="#">HOME</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#service">SERVICES</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#about">ABOUT</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#product">PRODUCT</a>
              </li>
              <li class="nav-item">
                <a class="nav-link position-relative" href="#">
                  <i class="fad fa-shopping-cart fa-1x"></i>
                  <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
                    {{ cart }}
                    <span class="visually-hidden">unread messages</span>
                  </span>
                </a>
              </li>
              <li class="nav-item ms-5">
                <button type="button" class="btn btn-outline-dark" data-bs-toggle="modal" data-bs-target="#exampleLocation">Add Location
                </button>
              </li>
            </ul>
          </div>
        </div>
    </nav>
    <!-- end -->

    <!-- Modal Add Location -->
    <div class="modal fade" id="exampleLocation" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog modal-xl">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Location</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <button class="btn btn-primary" type="button" data-bs-toggle="collapse" data-bs-target="#collapseExample" aria-expanded="false" aria-controls="collapseExample">
              Add
            </button>
            <CustTable v-bind:customers='customers' 
            @edit-address="editAddress"
            @delete-address="deleteAddress"
            />

            <div class="collapse" id="collapseExample">
              <div class="card card-body">
                <FormCust @add-address="addAddress" />
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Save changes</button>
          </div>
        </div>
      </div>
    </div>
    <!-- end -->

  <!-- banner -->
    <div class="banner w-100 vh-100 d-flex justify-content-center align-items-center">
          <div class="container col-md-9 text-left">
              <h4 class="display-6">Welcome to our website</h4>
              <h5 class="display-1 fw-bold">Shopping Time</h5>
              <a href="#product">
                  <button class="btn btn-success btn-lg" type="button">Cek Product</button>
              </a>
          </div>
    </div>
  <!-- end -->

    <!-- service -->
    <div class="container-fluid service pt-5 pb-5">
        <div class="container text-center">
            <h5 class="text-secondary" id="service">SERVICES</h5>
            <h3 class="fw-bold">We Offer Best Services</h3>
            <i class="fal fa-heart-rate fa-2x"></i>
            <div class="row col-lg-12 pt-5">
              <div class="col-md-3">
                  <i class="fad fa-shipping-fast fa-3x"></i>
                  <h4 class="mt-3 fw-bold">Fast</h4>
                  <p class="text-left">Lorem ipsum dolor sit amet consectetur adipisicing elit. Possimus, maiores!</p>
              </div>
              <div class="col-md-3">
                  <i class="fad fa-hand-holding-box fa-3x"></i>
                  <h4 class="mt-3 fw-bold">COD</h4>
                  <p class="text-left">Lorem ipsum dolor sit amet consectetur adipisicing elit. Possimus, maiores!</p>
              </div>
              <div class="col-md-3">
                  <i class="fad fa-shield-alt fa-3x"></i>
                  <h4 class="mt-3 fw-bold">Safe</h4>
                  <p class="text-left">Lorem ipsum dolor sit amet consectetur adipisicing elit. Possimus, maiores!</p>
              </div>
              <div class="col-md-3">
                  <i class="fad fa-box-check fa-3x"></i>
                  <h4 class="mt-3 fw-bold">Good Quality</h4>
                  <p class="text-left">Lorem ipsum dolor sit amet consectetur adipisicing elit. Possimus, maiores!</p>
              </div>
            </div>
        </div>
    </div>
    <!-- end -->

    <!-- about -->
    <div class="container-fluid pt-5 pb-5 bg-light shadow-lg">
        <div class="container">
          <div class="row col-lg-12 pt-5 align-items-center">
            <div class="col-md-1"></div>
            <div class="col-md-5">
              <h5 class="text-secondary" id="about">ABOUT</h5>
              <h3 class="fw-bold">About Us</h3>
              <i class="fal fa-heart-rate fa-2x"></i>
              <p class="pt-4">Lorem ipsum dolor sit amet consectetur adipisicing elit. Est pariatur consectetur veniam natus ut impedit iste, repudiandae harum autem libero.</p>
            </div>
            <div class="col-md-6">
              <img class="rounded mx-auto d-block" src="../assets/images/about2.jpg" width="400px" height="300px">
            </div>
            <div class="col-md-2"></div>
          </div>
        </div>
    </div>
    <!-- end -->

    <!-- Modal View Product -->
    <ProductPopUp 
    :product="product"
    :active="active.product_popUp"
    v-on:close-product-popUp="closeProductPopUp()"
    v-on:add-cart="addCart()"
    v-on:del-cart="delCart()"
    />
    <!-- end -->

    <!-- product -->
    <div class="container-fluid pt-5 pb-5">
        <div class="container text-center">
          <h5 class="text-secondary" id="product">PRODUCT</h5>
          <h3 class="fw-bold">Our Best Products</h3>
          <i class="fal fa-heart-rate fa-2x"></i>
          <div class="row col-md-12 pt-5">
            <ProductDisplay
            v-for="product in items"
            :key="product.id"
            :product="product"
            v-on:view-product="viewProduct($event)"
            />
          </div>
        </div>
    </div>
    <!-- end -->
    <FooterDisplay />
    <!-- footer -->
    
    <!-- end -->
</template>