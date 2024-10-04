<template>
    <v-card v-if="pokemon.name"
        class="mx-auto card pokemon-cards ma-2 rounded-xl bg-grey-lighten-2 d-col-flex align-center ga-9">
        <div class="d-flex justify-center">
            <v-img v-bind:src="pokemon.img" height="200px"></v-img>
        </div>
        <v-card-title class="text-center text-h4">
            {{ pokemon.name }}
        </v-card-title>
        <v-card-subtitle class="text-center">
            #{{ pokemon.id }}
        </v-card-subtitle>
        <h1> </h1>
        <v-card-text>
            <v-card class="mx-auto pa-3">
                <div>
                    <h3 class="text-center text-h5">Estatisticas</h3>
                </div>
                <v-spacer></v-spacer>
                <div class="d-flex justify-center flex-wrap text-body-1">
                    <ul>
                        <li> HP : {{ pokemon.hp }} </li>
                        <li> Ataque : {{ pokemon.attack }}</li>
                        <li> Defesa : {{ pokemon.defense }}</li>
                        <li> Ataque Especial : {{ pokemon.sAttack }}</li>
                        <li> Defesa Especial : {{ pokemon.sDefense }}</li>
                        <li> Velocidade : {{ pokemon.speed }}</li>
                    </ul>
                </div>
            </v-card>
            <v-card class="mx-auto pa-3 mt-3">
                <div>
                    <h3 class="text-center text-h5">Evoluções</h3>
                </div>
                <v-spacer></v-spacer>
                <div class="d-flex justify-center flex-wrap text-body-1">
                </div>
            </v-card>
        </v-card-text>
    </v-card>

    <v-card v-else class="mx-auto card pokemon-cards ma-2 rounded-xl bg-grey-lighten-2 d-col-flex align-center ga-9">
        <div class="d-flex justify-center align-center fill-height">
            <v-img src="../assets/pokedex.png" max-width="150px"></v-img>
            <v-card-title class="text-center">
                Selecione um Pokemon
            </v-card-title>
        </div>
        <v-card-subtitle class="text-center">
        </v-card-subtitle>
        <h1> </h1>
        <v-card-text>

        </v-card-text>
    </v-card>
</template>

<script lang="ts" setup>
const pokemon = defineProps(['name', 'id', 'img', 'hp', 'attack', 'defense', 'sAttack', 'sDefense', 'speed'
])
console.log(pokemon.hp)

//
</script>