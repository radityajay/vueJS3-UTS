<script>
export default{
    data(){
        return{
          // id: , //randomly generated id
            customer: {
                id: Math.ceil(Math.random()*1000000),
                name: '',
                kode: '',
                alamat: ''
            }
        }
    },
    methods:{
        submit(){
            this.$emit('add-address', this.customer)
            this.customer = {
                id: Math.ceil(Math.random()*1000000),
                name: '',
                kode: '',
                alamat: '',
            }
        }
    }
}
</script>
<template>
<form class="row g-3" @submit.prevent="submit">
  <input type="hidden" v-model="customer.id" class="form-control" id="name">
  <div class="col-md-6">
    <label for="name" class="form-label">Name</label>
    <input type="text" v-model="customer.name" class="form-control" id="name">
  </div>
  <div class="col-md-6">
    <label for="kode" class="form-label">Code Post</label>
    <input type="text" v-model="customer.kode" class="form-control" id="kode">
  </div>
  <div class="col-12">
    <label for="alamat" class="form-label">Address</label>
    <input type="text" v-model="customer.alamat" class="form-control" id="alamat" placeholder="Jl. Kambang">
  </div>
  <div class="col-12">
    <button type="submit" class="btn btn-primary">Add</button>
  </div>
</form>
</template>