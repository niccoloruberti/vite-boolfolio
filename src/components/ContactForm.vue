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
            errors: []
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
            };
            // pulisco l'array degli errori
            this.errors = [];

            axios.post(`${this.store.baseUrl}/api/contacts`, data).then((response) => {
                this.success = response.data.success;
                if(!this.success) {
                    this.errors = response.data.errors;
                    console.log(this.errors);
                } else {
                    //ripulisco i dati in inpute
                    this.name = '',
                    this.email = '',
                    this.message = '';

                    this.$router.push({name: 'thank-you'})
                }
            })
        }
    },
}
</script>

<template lang="">
    <div>
        <div class="py-5">
            <div class="container">
                <div class="row">
                    <div class="col-12">
                        <h2 class="text-center">Contattaci</h2>
                    </div>
                    <div v-if="success" class="col-12">
                        <div class="alert alert-success">
                            Messaggio inviato con successo
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-12">
                            <p v-for="(error, index) in errors" :key="index" class="text-danger">
                                        {{ error }}
                            </p>
                            <form @submit.prevent="sendForm()" class="row">
                                <div class="col-12 col-md-6">
                                    <label class="control-label">Nome e Cognome</label>
                                    <input type="text" name="name" id="name" v-model="name" placeholder="Name" class="form-control" :class="errors.name ? 'is-invalid' : ''">
                                </div>
                                <div class="col-12 col-md-6">
                                    <label class="control -label">Email</label>
                                    <input type="mail" name="email" id="email" v-model='email' placeholder="Email" class="form-control" :class="errors.email ? 'is-invalid' : ''">
                                </div>
                                <div class="col-12">
                                    <label class="contorl-label">Contenuto</label>
                                    <textarea class="form-control" name="content" id="content" v-model="message" placeholder="Messaggio" :class="errors.content ? 'is-invalid' : ''" cols="30" rows="10"></textarea>
                                </div>
                                <div class="col-12">
                                    <button class="btn btn-success" type="submit">Invia</button>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="">
    
</style>