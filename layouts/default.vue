<template>
  <v-app>
    <!-- <AppBar :drawer="isDrawerShown" @toggle-drawer="toggleDrawer" /> -->
    <v-main>
      <nuxt />
    </v-main>
    <NavDrawer :showDrawer="isDrawerShown" @toggle-drawer="toggleDrawer" />
    <v-btn
      @click.stop="toggleDrawer"
      class="secondary--text ma-8"
      color="white"
      elevation="2"
      large
      rounded
      fixed
      top
      right
    >
      Navigation
      <v-icon right>mdi-menu</v-icon>
    </v-btn>
  </v-app>
</template>

<script>
import AppBar from '~/components/layout/AppBar.vue'
import Footer from '~/components/Footer.vue'

export default {
  components: {
    AppBar,
    Footer,
  },
  data: () => {
    return {
      drawer: false,
      title: 'Frühförderstelle Teddybär',
      navLinks: [
        {
          icon: 'mdi-newspaper',
          color: 'red lighten-2',
          title: 'News',
          to: '/news',
        },
        {
          icon: 'mdi-train-car',
          color: 'amber darken-1',
          title: 'Anfahrt',
          to: '/#anfahrt',
        },
        {
          icon: 'mdi-mailbox',
          color: 'light-green lighten-1',
          title: 'Kontakt',
          to: '/#kontakt',
        },
      ],
    }
  },
  computed: {
    isDrawerShown() {
      return this.$nuxt.$vuetify.breakpoint.lgAndUp ? true : this.drawer
    },
  },
  methods: {
    toggleDrawer(newState) {
      this.drawer = newState
    },
  },
}
</script>
