<script>
export default{
    props: {
        customers: Array
    },
    data(){
        return{
            customerId: null
        }
    },
    methods:{
        editAddress(customer) { 
          this.data = Object.assign({}, customer)
          this.customerId = customer.id 
          // console.log(this.data);
        },
        saveEdit(customer) { 
          let id = this.data.id
          this.$emit('edit-address', id, customer)  
          this.customerId = null
        },
        cancelEdit(customer) { 
          Object.assign(customer, this.data)
          this.customerId = null;
          // console.log(this.customerId);
        },
        deleteAddress(id){
          this.$emit('delete-address', id)  
        }
    }
}
</script>
<template>
<table class="table table-striped">
    <thead class="table-light">
        <td>Name</td>
        <td>Kode</td>
        <td>Address</td>
    </thead>
    <tbody>
        <tr v-for="customer in customers" :key="customer.id">
            <template v-if="customerId === customer.id">
                <td>
                    <label for="name" class="form-label">Name</label>
                    <div>
                        <input type="text" v-model="customer.name" class="form-control" id="name">
                    </div>
                </td>
                <td>
                    <label for="kode" class="form-label">Code Post</label>
                    <div>
                        <input type="text" v-model="customer.kode" class="form-control" id="kode">
                    </div>
                </td>
                <td>
                    <label for="alamat" class="form-label">Address</label>
                    <div>
                        <input type="text" v-model="customer.alamat" class="form-control" id="alamat">
                    </div>
                </td>
                <td>
                    <div class="mt-4">
                        <button class="btn btn-success m-2" @click="saveEdit(customer)">Save</button>
                        <button class="btn btn-danger" @click="cancelEdit(customer)" >Cancel</button>
                    </div>
                </td>
            </template>
            <template v-else>
                <td>{{ customer.name }}</td>
                <td>{{ customer.kode }}</td>
                <td>{{ customer.alamat }}</td>
                <td>
                    <div class="text-center">
                    <button class="btn btn-primary me-2" @click="editAddress(customer)">Edit</button>
                    <button class="btn btn-danger" @click="deleteAddress(customer.id)">Hapus</button> 
                    </div>
                </td>
            </template>
        </tr>
    </tbody>
</table>
</template>