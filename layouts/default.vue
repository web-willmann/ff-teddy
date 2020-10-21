<template>
  <v-app>
    <AppBar :drawer="isDrawerShown" @toggle-drawer="toggleDrawer" />
    <v-main>
      <nuxt />
    </v-main>
    <NavDrawer :showDrawer="isDrawerShown" @toggle-drawer="toggleDrawer" />
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
