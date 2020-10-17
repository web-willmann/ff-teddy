<template>
  <v-app-bar style="z-index: 98" elevation="2" fixed app>
    <div class="branding" @click.stop="clickBranding">
      <v-avatar class="mr-4" size="36" tile>
        <v-img :src="require('~/assets/teddy_icon.svg')"></v-img>
      </v-avatar>
      <v-toolbar-title v-text="title" />
    </div>
    <v-spacer />
    <v-app-bar-nav-icon
      v-if="!drawer"
      @click.stop="$emit('toggleDrawer', true)"
    />
  </v-app-bar>
</template>

<script>
export default {
  props: {
    drawer: {
      type: Boolean,
      default: false,
    },
  },
  data: () => {
    return {
      title: 'Frühförderstelle Teddybär',
    }
  },
  methods: {
    clickBranding: function () {
      if (this.$route.name == 'index') {
        this.$vuetify.goTo(0)
        this.$router.push('/')
      } else {
        this.$router.push('/')
      }
    },
  },
}
</script>

<style>
.branding {
  display: flex;
  align-items: center;
  cursor: pointer;
}
</style>