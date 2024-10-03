<template>
    <v-card v-if="pokemon.name" class="mx-auto card pokemon-cards ma-2 rounded-xl bg-grey-lighten-2 d-col-flex align-center ga-9">
        <v-img v-bind:src="pokemon.img" max-width="150px"></v-img>
        <v-card-title class="text-center">
            {{ pokemon.name}}
        </v-card-title>
        <v-card-subtitle class="text-center">
            #{{ pokemon.id }}
        </v-card-subtitle>
        <h1> </h1>
        <v-card-text class="btn-info">

        </v-card-text>
    </v-card>

    <v-card v-else class="mx-auto card pokemon-cards ma-2 rounded-xl bg-grey-lighten-2 d-col-flex align-center ga-9">
        <v-img src="../assets/pokedex.png" max-width="150px"></v-img>
        <v-card-title class="text-center">
            Selecione um Pokemon
        </v-card-title>
        <v-card-subtitle class="text-center">
        </v-card-subtitle>
        <h1> </h1>
        <v-card-text class="btn-info">

        </v-card-text>
    </v-card>
</template>

<script lang="ts" setup>
import {ref, reactive} from 'vue'
const pokemon = defineProps(['name', 'id', 'img']) 
console.log(pokemon)

//
</script>