<template>
  <v-navigation-drawer
    style="z-index: 99"
    v-model="isActive"
    disable-resize-watcher
    disable-route-watcher
    right
    app
  >
    <v-app-bar elevation="2">
      <v-toolbar-title>{{ title }}</v-toolbar-title>
      <v-spacer />
      <v-btn
        v-if="!this.$vuetify.breakpoint.lgAndUp"
        large
        @click.stop="isActive = false"
        icon
        ><v-icon>mdi-close</v-icon></v-btn
      >
    </v-app-bar>
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
</template>

<script>
export default {
  props: {
    showDrawer: {
      type: Boolean,
      required: true,
    },
  },
  data: () => {
    return {
      isActive: false,
      title: 'Navigation',
      navLinks: [
        {
          icon: 'mdi-home',
          color: 'blue lighten-2',
          title: 'Start',
          to: '/',
        },
        {
          icon: 'mdi-newspaper',
          color: 'red lighten-2',
          title: 'News',
          to: '/news/1',
        },
      ],
    }
  },
  watch: {
    showDrawer: function () {
      this.isActive = this.showDrawer
    },
    isActive: function (val) {
      this.$emit('toggle-drawer', val)
    }
  }
}
</script>