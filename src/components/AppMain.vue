<script>
import axios from 'axios';
export default {
    name: 'AppMain',
    data() {
        return{
            baseUrl: 'http://localhost:8000',
            projects: [],
        }
    },
    created(){
        this.getProjects();
    },
    methods:{
        getProjects() {
            axios.get(`${this.baseUrl}/api/projects`).then((response) => {
                if(response.data.success) {
                    this.projects = response.data.results;
                } else {

                }
            })
        }
    }
}
</script>

<template>
  <div>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <h1 class="text-center">Boolfolio</h1>
            </div>
        </div>
    </div>
    <div class="container">
        <div class="row">
            <div class="col-12 col-md-4" v-for="project in projects" :key="project.id">
                <div class="card">
                    <div class="card-image-top">
                        <img class="img-height img-fluid" :src="`${baseUrl}/storage/${project.img}`">
                    </div>
                    <div class="card-header">{{ project.name }}</div>
                    <div class="card-body">
                        <p>Argomento: <span>{{ project.topic }}</span></p>
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
  </div>
</template>

<style>

.img-height {
    max-height: 300px;
}

</style>
