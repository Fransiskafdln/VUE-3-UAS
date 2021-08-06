<template>
        <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link 
                    :to="{ name: 'edit.index'}"
                    class="btn btn-primary btn-sm rounded shadow mb-3"

                > Back</router-link>

                <div class="card rounded shadow">
                    <div class="card-header">
                        Kontak Edit 
                    </div>

                    <div class="card-body">
                       <form @submit.prevent="store()">
                           <div class="mb-3">
                               <label for="" class="form-label">Nomor Telepon</label>
                               <input type="text" class="form-control" v-model="edit.no_tlp">
                               <div v-if="validation.no_tlp" class="text-danger">
                                   {{ validation.no_tlp [0] }}
                               </div>
                           </div>

                           <div class="mb-3">
                               <label for="" class="form-label">Email</label>
                               <input type="text" class="form-control" v-model="edit.email">
                               <div v-if="validation.email" class="text-danger">
                                   {{ validation.email [0] }}
                               </div>
                           </div>

                           <div class="mb-3">
                               <label for="" class="form-label">Instagram</label>
                               <input type="text" class="form-control" placeholder="Instagram" v-model="edit.instagram">
                               <div v-if="validation.instagram" class="text-danger">
                                   {{ validation.instagram [0] }}
                               </div>
                           </div>

                           <button class="btn btn-outline-primary">Submit</button>
                       </form>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>


<script>
import {reactive, ref} from 'vue'
import { useRouter } from 'vue-router'
import axios from 'axios'
export default {
     setup () {
        //  data binding
        const kontak = reactive({
            no_tlp: '',
            email: '',
            instagram: '',
        });
        const validation = ref ([]);
        const router = useRouter();
        function store(){
            axios.post(
                'http://127.0.0.1:8000/api/kontak',
                kontak
            )
            .then((result) => {
                router.push({
                    name: 'kontak.index'
                });
            }) .catch((err) => {
                validation.value = err.response.data
            });
        }
        return {
            kontak,
            validation,
            router,
            store
        }
     }
}
</script>