<template>
    <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link 
                    :to="{ name: 'kerja.create'}"
                    class="btn btn-primary btn-sm rounded shadow mb-3"

                > Add</router-link>

                <div class="card rounded shadow">
                    <div class="card-header">
                        Pengalaman Kerja
                    </div>

                    <div class="card-body">
                        <table class="table">
                            <thead>
                                <th>Nama Perusahaan</th>
                                <th>Bagian</th>
                                <th>Tahun Kerja</th>
                                                                                                
                            </thead>

                            <tbody>
                                <tr v-for="(kerja, index) in kerjas.data" :key="index">
                                    <td>{{ kerja.perusahaan}}</td>
                                    <td>{{kerja.bagian}}</td>
                                    <td>{{kerja.th_kerja}}</td>
                                    <td>
                                        <div class="btn-group">
                                            <router-link
                                                :to="{ name:'kerja.edit', params:{id: kerja.id}}"
                                                class="btn btn-sm btn-outline-info"
                                            >Edit</router-link>
                                            <button class="btn btn-sm btn-outline-danger">
                                                Delete
                                            </button>
                                        </div>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>

<script>
import axios from 'axios'
import {onMounted, ref} from 'vue'
export default {
    setup () {
        // reactive state
        let kerja = ref([]);
        onMounted(() => {
            // get data from api endpoint
        axios.get('http://127.0.0.1:8000/api/kerja')
        .then((result)  => {
            kerjas.value = result.data
        }).catch((err) => {
            console.log(err.response)
        });
        });
    return {
        kerjas
        }
    }
}
</script>