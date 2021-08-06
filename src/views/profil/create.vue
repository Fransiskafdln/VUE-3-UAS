<template>
        <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link 
                    :to="{ name: 'profil.index'}"
                    class="btn btn-primary btn-sm rounded shadow mb-3"

                > Back</router-link>

                <div class="card rounded shadow">
                    <div class="card-header">
                        Create Profil List
                    </div>

                    <div class="card-body">
                       <form @submit.prevent="store()">
                           <div class="mb-3">
                               <label for="" class="form-label">Nama</label>
                               <input type="text" class="form-control" v-model="profil.title">
                               <div v-if="validation.nama" class="text-danger">
                                   {{ validation.nama [0] }}
                               </div>
                           </div>

                           <div class="mb-3">
                               <label for="" class="form-label">Tempat, Tanggal Lahir</label>
                               <input type="text" class="form-control" v-model="profil.ttl">
                               <div v-if="validation.ttl" class="text-danger">
                                   {{ validation.ttl [0] }}
                               </div>
                           </div>

                           <div class="mb-3">
                               <label for="" class="form-label">Staus</label>
                               <input type="text" class="form-control" placeholder="Instagram" v-model="profil.status">
                               <div v-if="validation.status" class="text-danger">
                                   {{ validation.status [0] }}
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
        const profil = reactive({
            nama: '',
            ttl: '',
            status: '',
        });
        const validation = ref ([]);
        const router = useRouter();
        function store(){
            axios.post(
                'http://127.0.0.1:8000/api/profil',
                profil
            )
            .then((result) => {
                router.push({
                    name: 'profil.index'
                });
            }) .catch((err) => {
                validation.value = err.response.data
            });
        }
        return {
            profil,
            validation,
            router,
            store
        }
     }
}
</script>