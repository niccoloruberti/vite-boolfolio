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
                console.log(response.data.success);

                if(response.data.success) {
                    console.log(response.data.success);
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
    <div>
        prova
    </div>
</template>

<style lang="">
    
</style>