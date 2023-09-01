<script>
import axios from 'axios';
import { store } from '../store.js';
export default {
    name: 'ContactForm',
    data(){
        return {
            store,
            name: '',
            email: '',
            message: '',
            success: false,
            errors: {}
        }
    },
    components: {

    },
    methods: {
        sendForm(){
            const data = {
                name: this.name,
                email: this.email,
                content: this.message,
            }
            // pulisco l'array degli errori
            this.errors = {};

            axios.post(`${this.store.baseUrl}/api/contacts`, data).then((response) => {
                this.success = response.data.success;
                if(!this.success) {
                    this.errors = response.data.errors;
                } else {
                    //ripulisco i dati in inpute
                    this.name = '',
                    this.email = '',
                    this.message = '';
                }
            })
        }
    },
}
</script>

<template lang="">
    <div>
        
    </div>
</template>

<style lang="">
    
</style>