<script>
export default{
    props: ['product'],
    computed: {
        image(){
            return this.product.image
        }
    }
}
</script>

<template>
    <div class="col-md-4 mb-4">
        <div class="card overflow-hidden shadow radius" style="width: 90%;">
            <img v-bind:src="image" class="card-img-top" alt="...">
            <div class="card-body py-4 px-3">
                <div class="d-flex flex-column flex-lg-row justify-content-between mb-3">
                    <h4 class="text-secondary fw-medium">
                        <a class="text-decoration-none ft-color" href="#!">{{ product.name }}</a>
                    </h4>
                    <h4 class="text-secondary">Rp.{{ product.price.toFixed(3) }}</h4>
                </div>
                <div class="d-flex align-items-center"> 
                    <i class="fad fa-star fa-1x" style="color: #FFC943;"></i>
                    <span class="fs-0 fw-medium"> 5.00</span>
                </div>
                <!-- <button class="btn btn-success mx-2" v-on:click="addToCart">BUY</button> -->
                <button class="btn btn-primary" @click="$emit('view-product', product)" data-bs-toggle="modal" data-bs-target="#exampleModal">VIEW</button>
            </div>
        </div> 
    </div>
</template>