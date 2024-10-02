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
        </v-toolbar>
    </v-card>
</template>
<script>

</script>

<style>
.toolbar{
    width: 39rem !important;
}
.v-toolbar__content{
    justify-content: center;
}
</style>