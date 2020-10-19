<template>
  <v-app-bar style="z-index: 98" elevation="2" fixed app>
    <div class="branding" @click.stop="clickBranding">
      <v-avatar class="mr-4" size="36" tile>
        <v-img :src="require('~/assets/teddy_icon.svg')"></v-img>
      </v-avatar>
      <v-toolbar-title v-text="title" />
    </div>
    <v-spacer />
    <v-btn v-if="this.$route.name == 'news-post-postId'" color="blue-grey lighten-1 white--text" @click.stop="$router.go(-1)" depressed
      >Zurück</v-btn
    >
    <v-btn v-if="this.$route.name == 'news-pageNr'" color="blue-grey lighten-1 white--text" to="/" depressed
      >Zurück</v-btn
    >
    <v-app-bar-nav-icon
      v-if="!drawer"
      class="ml-2"
      @click.stop="$emit('toggle-drawer', true)"
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
      prevRoute: '',
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