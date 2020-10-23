<template>
    <v-row class="ma-4" justify="center">
        <v-col cols="12" lg="10" xl="8">
            <v-img :src="require('~/assets/images/hero-bg.jpg')" class="d-flex align-center" height="400px" cover>
                <div class="title-font black--text text-center">Frühförderstelle</div>
                <div class="title-font secondary--text text-center">Teddybär</div>
                <v-img class="mt-6" max-width="100%" max-height="9px" :src="require('~/assets/images/dots-divider.svg')" contain></v-img>
            </v-img>
        </v-col>
    </v-row>
</template>

<style scoped>
.title-font {
    font-size: 3rem;
    font-family: 'Subscriber', sans-serif;
}
</style>