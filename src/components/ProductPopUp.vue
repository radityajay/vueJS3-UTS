<script>

export default{
    name: 'ProductPopUp',
    components: {

    },
    props: ['product', 'active'],
    computed:{
        product_total(){
            return
        }
    }
}
</script>
<template>
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true" :class="{show: active}" @click="$emit('close-product-popUp')">
        <div class="modal-dialog modal-xl">
            <div class="modal-content" v-if="product">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">{{product.category}}</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" @click="$emit('close-product-popUp')"></button>
                </div>
                <div class="modal-body">
                    <div class="container-fluid">
                        <div class="row">
                            <div class="col-md-5 me-5">
                                <img v-bind:src="product.image" class="card-img-top" alt="..." width="100" height="550">
                            </div>
                            <div class="col-md-6 text-justify">
                                <h3 class="">{{product.name}}</h3>
                                <h5 class="text-secondary pt-2">{{product.category}}</h5>
                                <p class="pt-3">{{product.desc}}</p>
                                <h4 class="fw-medium fw-bold pt-2">Rp.{{ product.price.toFixed(3) }}</h4>
                                <div class="cart-total mt-5 text-center" v-if="product_total">
                                    <h3 class="fw-bold">In Cart</h3>
                                    <h4>{{product_total}}</h4>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <div class="text-center">
                        <button type="button" class="btn btn-success mx-2" v-on:click="$emit('add-cart')">BUY</button>
                        <button type="button" class="btn btn-danger" v-on:click="$emit('del-cart')">CANCEL</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>