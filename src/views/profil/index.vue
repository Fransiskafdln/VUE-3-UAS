<template>
    <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link 
                    :to="{ name: 'profil.create'}"
                    class="btn btn-primary btn-sm rounded shadow mb-3"

                > Add</router-link>

                <div class="card rounded shadow">
                    <div class="card-header">
                        profil List
                    </div>

                    <div class="card-body">
                        <table class="table">
                            <thead>
                                <th>Nama</th>
                                <th>Tempat, Tanggal Lahir</th>
                                <th>Status</th>
                            </thead>

                            <tbody>
                                <tr v-for="(profil, index) in profils.data" :key="index">
                                    <td>{{ profil.nama}}</td>
                                    <td>{{profil.ttl}}</td>
                                    <td>{{profil.status}}</td>
                                    <td>
                                        <div class="btn-group">
                                            <router-link
                                                :to="{ name:'profil.edit', params:{id: profil.id}}"
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
        let profil = ref([]);
        onMounted(() => {
            // get data from api endpoint
        axios.get('http://127.0.0.1:8000/api/profil')
        .then((result)  => {
            profils.value = result.data
        }).catch((err) => {
            console.log(err.response)
        });
        });
    return {
        profils
        }
    }
}
</script>