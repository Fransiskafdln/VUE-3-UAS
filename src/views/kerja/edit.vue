<template>
        <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link 
                    :to="{ name: 'kerja.index'}"
                    class="btn btn-primary btn-sm rounded shadow mb-3"

                > Back</router-link>

                <div class="card rounded shadow">
                    <div class="card-header">
                        Create Pengalaman Kerja
                    </div>

                    <div class="card-body">
                       <form @submit.prevent="store()">
                           <div class="mb-3">
                               <label for="" class="form-label">Perusahaan</label>
                               <input type="text" class="form-control" v-model="type.perusahaan">
                               <div v-if="validation.perusahaan" class="text-danger">
                                   {{ validation.perusahaan [0] }}
                               </div>
                           </div>

                           <div class="mb-3">
                               <label for="" class="form-label">Bagian</label>
                               <input type="text" class="form-control" v-model="kerja.bagian">
                               <div v-if="validation.bagian" class="text-danger">
                                   {{ validation.bagian [0] }}
                               </div>
                           </div>

                           <div class="mb-3">
                               <label for="" class="form-label">Tahun Lulus</label>
                               <input type="text" class="form-control" placeholder="Tahun Lulus" v-model="kerja.th_kerja">
                               <div v-if="validation.th_kerja" class="text-danger">
                                   {{ validation.th_kerja [0] }}
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
        let kerja = reactive({
            perusahaan:   '',
            bagian:  '',
            th_kerja:    '',
        });
        const validation = ref ([]);
        const router = useRouter();
        const route = useRoute();
        onMounted(() => {
            axios.get('http://127.0.0.1:8000/api/kerja/${route.params.id}')
            .then((result) => {
                kerja.perusahaan = result.data.data.perusahaan
                kerja.bagian = result.data.data.bagian
                kerja.th_kerja = result.data.data.th_kerja
            }).catch((err) => {
                console.log(err.response.data)
            });
        });
        function update(){
            axios.post(
                'http://127.0.0.1:8000/api/kerja',
                kerja
            )
            .then((result) => {
                router.push({
                    name: 'kerja.index'
                });
            }) .catch((err) => {
                validation.value = err.response.data
            });
        }
        return {
            kerja,
            validation,
            router,
            update
        
        }
     }
}
</script>