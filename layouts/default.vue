<template>
  <v-app dark>
    <v-app-bar fixed app>
      <v-avatar class="mr-4" size="36" tile>
        <v-img :src="require('~/assets/teddy_icon.svg')"></v-img>
      </v-avatar>
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <span class="d-none d-md-inline" v-for="(item, i) in navLinks" :key="i">
        <v-btn
          class="ml-4 white--text"
          :color="item.color"
          :to="item.to"
          light
          depressed
          large
        >
          <v-icon color="white" left>{{ item.icon }}</v-icon>
          {{ item.title }}
        </v-btn>
      </span>
      <v-app-bar-nav-icon
        class="d-md-none"
        v-if="!drawer"
        @click.stop="drawer = true"
      />
      <v-app-bar-nav-icon
        class="d-md-none"
        v-if="drawer"
        @click.stop="drawer = false"
      >
        <v-icon>mdi-close</v-icon>
      </v-app-bar-nav-icon>
    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
    <!-- :value="isDrawerShown"
    @input="updateDrawer" -->
    <v-navigation-drawer v-model="drawer" right app>
      <v-list>
        <v-row class="px-8" align="center">
          <h6 class="text-h6">Navigation</h6>
          <v-spacer></v-spacer>
          <v-btn large @click.stop="drawer = false" icon
            ><v-icon>mdi-close</v-icon></v-btn
          >
        </v-row>
        <v-divider class="my-2"></v-divider>
        <v-list-item
          v-for="(item, i) in navLinks"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon :color="item.color">{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <Footer />
  </v-app>
</template>

<script>
import Footer from '~/components/Footer.vue'

export default {
  components: {
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
      return this.$nuxt.$vuetify.breakpoint.mdAndUp ? false : this.drawer
    },
  },
  methods: {
    updateDrawer(newState) {
      this.drawer = newState
    },
  },
}
</script>
