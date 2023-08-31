<script>
import axios from 'axios'
import { store } from '../store.js'
import { router } from '../router.js'
export default {
    name: 'SingleProject',
    data() {
        return {
            store,
            project: null
        }
    },
    created() {
        this.getSinglesProject()
    },
    methods: {
        getSinglesProject() {
            axios.get(`${this.store.baseUrl}/api/projects/${this.$route.params.slug}`).then((response) => {
                if(response.data.success) {
                    this.project = response.data.project;
                } else {
                    this.$router.push({name: 'not-found'});
                }
            })
        }
    },
}
</script>

<template lang="">
    <div class="container">
        <div class="row">
            <div class="mt-5 col-12">
                <div class="card">
                    <div class="card-image-top">
                        <img class="img-height img-fluid" :src="`${this.store.baseUrl}/storage/${project.img}`">
                    </div>
                    <div class="card-header">{{ project.name }}</div>
                    <div class="card-body">
                        <p>Argomento: <span>{{ project.topic }}</span></p>
                        <p>Link repository: <span>{{ project.link_repository }}</span></p>
                        <!-- tipologia progetto -->
                        <p v-if="project.type">Tipologia: <span>{{ project.type.name }}</span></p>
                        <!-- tecnologie utilizzate -->
                        <div v-if="(project.technologies.length > 0)">
                            <span><strong>Tecnologie utilizzate:</strong></span>
                            <ul>
                                <li v-for="technology in project.technologies" :key="technology.id">
                                    {{ technology.name }}
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="">
    
</style>