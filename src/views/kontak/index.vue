<template>
    <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link 
                    :to="{ name: 'kontak.create'}"
                    class="btn btn-primary btn-sm rounded shadow mb-3"

                > Add</router-link>

                <div class="card rounded shadow">
                    <div class="card-header">
                        Contact Me
                    </div>

                    <div class="card-body">
                        <table class="table">
                            <thead>
                                <th>No Telepon</th>
                                <th>Email</th>
                                <th>Instagram</th>
                            </thead>

                            <tbody>
                                <tr v-for="(kontak, index) in kontaks.data" :key="index">
                                    <td>{{ kontak.no_tlp}}</td>
                                    <td>{{kontak.email}}</td>
                                    <td>{{kontak.instagram}}</td>
                                    <td>
                                        <div class="btn-group">
                                            <router-link
                                                :to="{ name:'kontak.edit', params:{id: kontak.id}}"
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
        let kontak = ref([]);
        onMounted(() => {
            // get data from api endpoint
        axios.get('http://127.0.0.1:8000/api/kontak')
        .then((result)  => {
            kontaks.value = result.data
        }).catch((err) => {
            console.log(err.response)
        });
        });
    return {
        kontaks
        }
    }
}
</script>