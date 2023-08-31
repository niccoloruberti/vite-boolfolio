<script>
import { store } from '../store.js'
export default {
    name: 'ProjectCard',
    props: {
        project: Object
    },
    data(){
        return {
            store
        }
    }
}
</script>

<template lang="">
    <div class="card">
        <div class="card-image-top">
            <img class="img-height img-fluid" :src="`${this.store.baseUrl}/storage/${project.img}`">
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
            <div>
                <router-link :to="{name: 'single-project', params: { slug: project.slug}}" class="btn btn-primary">Vai al progetto</router-link>
            </div>
        </div>
    </div>
</template>

<style lang="">
    
</style>