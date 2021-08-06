<template>
    <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link 
                    :to="{ name: 'pendidikan.create'}"
                    class="btn btn-primary btn-sm rounded shadow mb-3"

                > Add</router-link>

                <div class="card rounded shadow">
                    <div class="card-header">
                        Riwayat Pendidikan
                    </div>

                    <div class="card-body">
                        <table class="table">
                            <thead>
                                <th>Tingkat Pendidikan</th>
                                <th>Sekolah</th>
                                <th>th Lulus</th>
                                                                                                
                            </thead>

                            <tbody>
                                <tr v-for="(pendidikan, index) in pendidikans.data" :key="index">
                                    <td>{{ pendidikan.type}}</td>
                                    <td>{{pendidikan.nama}}</td>
                                    <td>{{prpendidikanofil.th_lulus}}</td>
                                    <td>
                                        <div class="btn-group">
                                            <router-link
                                                :to="{ name:'pendidikan.edit', params:{id: pendidikan.id}}"
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
        let pendidikan = ref([]);
        onMounted(() => {
            // get data from api endpoint
        axios.get('http://127.0.0.1:8000/api/pendidikan')
        .then((result)  => {
            pendidikans.value = result.data
        }).catch((err) => {
            console.log(err.response)
        });
        });
    return {
        pendidikans
        }
    }
}
</script>