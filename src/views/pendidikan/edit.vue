<template>
        <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link 
                    :to="{ name: 'pendidikan.index'}"
                    class="btn btn-primary btn-sm rounded shadow mb-3"

                > Back</router-link>

                <div class="card rounded shadow">
                    <div class="card-header">
                        Create Riwayat Pendidikan
                    </div>

                    <div class="card-body">
                       <form @submit.prevent="store()">
                           <div class="mb-3">
                               <label for="" class="form-label">Tingkat Pendidikan</label>
                               <input type="text" class="form-control" v-model="type.title">
                               <div v-if="validation.type" class="text-danger">
                                   {{ validation.type [0] }}
                               </div>
                           </div>

                           <div class="mb-3">
                               <label for="" class="form-label">Sekolah</label>
                               <input type="text" class="form-control" v-model="pendidikan.nama">
                               <div v-if="validation.nama" class="text-danger">
                                   {{ validation.nama [0] }}
                               </div>
                           </div>

                           <div class="mb-3">
                               <label for="" class="form-label">Tahun Lulus</label>
                               <input type="text" class="form-control" placeholder="Tahun Lulus" v-model="pendidikan.th_lulus">
                               <div v-if="validation.th_lulus" class="text-danger">
                                   {{ validation.th_lulus [0] }}
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
import { reactive, ref, onMounted } from 'vue'
import { useRouter , useRoute } from 'vue-router'
import axios from 'axios'
export default {
     setup () {
        //  data binding
        let pendidikan = reactive({
            type:   '',
            nama:  '',
            th_lulus:    '',
        });
        const validation = ref ([]);
        const router = useRouter();
        const route = useRoute();
        onMounted(() => {
            axios.get('http://127.0.0.1:8000/api/pendidikan/${route.params.id}')
            .then((result) => {
                pendidikan.type = result.data.data.type
                pendidikan.nama = result.data.data.nama
                pendidikan.th_lulus = result.data.data.th_lulus
            }).catch((err) => {
                console.log(err.response.data)
            });
        });
        function update(){
            axios.post(
                'http://127.0.0.1:8000/api/pendidikan',
                pendidikan
            )
            .then((result) => {
                router.push({
                    name: 'pendidikan.index'
                });
            }) .catch((err) => {
                validation.value = err.response.data
            });
        }
        return {
            pendidikan,
            validation,
            router,
            update
        
        }
     }
}
</script>