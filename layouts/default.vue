<template>
  <v-app dark>
    <v-app-bar fixed dark color="transparent" flat>
      <v-avatar class="mr-4" tile>
        <v-img :src="require('~/assets/teddy_icon.svg')"></v-img>
      </v-avatar>
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <span
        class="d-none d-md-inline"
        v-for="(item, i) in navLinks"
        :key="i"
        :to="item.to"
      >
        <v-btn class="ml-4" color="white" light elevation="6" large>
          <v-icon :color="item.color" left>{{ item.icon }}</v-icon>
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
    <v-navigation-drawer
      :value="isDrawerShown"
      @input="updateDrawer"
      absolute
      stateless
      clipped
      right
      app
    >
      <v-list>
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
    <v-main>
      <nuxt />
    </v-main>
    <v-footer app>Footer.</v-footer>
  </v-app>
</template>

<script>
export default {
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
          to: '#anfahrt',
        },
        {
          icon: 'mdi-mailbox',
          color: 'light-green lighten-1',
          title: 'Kontakt',
          to: '#kontakt',
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