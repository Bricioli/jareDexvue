<template>
    <v-card class="rounded-pill ma-10 d-flex justify-center" flat color="transparent">
        <v-toolbar class="rounded-pill toolbar" dense floating color="primary">
            <v-btn class="rounded-pill" @click="$router.push('/')">
                Home
            </v-btn>
            <v-btn class="rounded-pill" @click="$router.push('/pokedex')">
                Pokedex
            </v-btn>
            <v-btn class="rounded-pill" @click="$router.push('/favoritos')">
                Favoritos
            </v-btn>
            <v-tooltip v-if="!theme.global.current.value.dark" bottom>
                <template v-slot:activator="{ on, attrs }">
                    <v-btn class="rounded-pill" v-on="on" v-bind="attrs" color="white" small fab @click="toggleTheme">
                        <v-icon class="mr-1">mdi-moon-waxing-crescent</v-icon>
                    </v-btn>
                </template>
                <span>Dark Mode Off</span>
            </v-tooltip>

            <v-tooltip v-else bottom>
                <template v-slot:activator="{ on, attrs }">
                    <v-btn class="rounded-pill" v-on="on" v-bind="attrs" color="white" small fab @click="toggleTheme">
                        <v-icon>mdi-white-balance-sunny</v-icon>
                    </v-btn>
                </template>
                <span>Dark Mode On</span>
            </v-tooltip>

        </v-toolbar>
    </v-card>
</template>
<script setup>
import { useTheme } from 'vuetify'


const theme = useTheme()

function toggleTheme() {
    theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'
    console.log(theme.global.name.value)
    console.log(theme.global.current.value.dark)

}

</script>

<style>
.toolbar {
    width: 39rem !important;
}

.v-toolbar__content {
    justify-content: center;
}
</style>