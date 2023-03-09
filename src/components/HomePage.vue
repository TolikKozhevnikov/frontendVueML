<template>
    <v-container>
        
        <v-col cols="4">
            <v-spacer></v-spacer>
             <p> {{ info }}</p>
        </v-col>

       
        <v-btn color="black" elevation="2" outlined class="text-uppercase" @onclick="login()">Выйти</v-btn>
    </v-container>
</template>

<script>

import axios from 'axios'

export default {
    data() {
        return {
            info: null
        };
    },
    mounted() {
        axios
            .get('https://api.coindesk.com/v1/bpi/currentprice.json')
            .then(response => (this.info = response));
    },

}
</script>

<style></style>