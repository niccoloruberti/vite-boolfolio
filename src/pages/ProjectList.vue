<script>
import axios from 'axios';
import ProjectCard from '../components/ProjectCard.vue';
export default {
    name: 'AppMain',
    data() {
        return{
            baseUrl: 'http://localhost:8000',
            projects: [],
            currentPage: 1,
            lastPage: null,
        }
    },
    components: {
        ProjectCard
    },
    created(){
        this.getProjects(1);
    },
    methods:{
        getProjects(numPage) {
            axios.get(`${this.baseUrl}/api/projects`, {params: {page: numPage}}).then((response) => {
                if(response.data.success) {
                    this.projects = response.data.results.data;
                    this.currentPage = response.data.results.current_page;
                    this.lastPage = response.data.results.last_page;
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
                <ProjectCard :project="project"/>
            </div>
        </div>
    </div>
    <div class="row">
        <div class="col-12">
            <div class="d-flex justify-content-center">
                <nav>
                    <ul class="pagination mt-3">
                        <li :class="currentPage === 1 ? 'disabled' : ''">
                            <button class="page-link" @click="getProjects(currentPage - 1)">Precedente</button>
                        </li>
                        <li :class="currentPage === lastPage ? 'disabled' : ''">
                            <button class="page-link" @click="getProjects(currentPage + 1)">Successivo</button>
                        </li>
                    </ul>
                </nav>
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
