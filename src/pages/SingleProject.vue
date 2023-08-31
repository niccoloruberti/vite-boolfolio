<script>
import axios from 'axios'
import { store } from '../store.js'
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
                }
            })
        }
    },
}
</script>

<template lang="">
    <div>
        prova
    </div>
</template>

<style lang="">
    
</style>