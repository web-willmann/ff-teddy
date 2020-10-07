<template>
  <div>
    <Banner />
    <v-container>
      <IntroSection /> <InfoSection />
      <LatestNewsSection :latestPost="latestPost" />
    </v-container>
  </div>
</template>

<script>
import Banner from '~/components/Banner.vue'
import IntroSection from '~/components/IntroSection.vue'
import InfoSection from '~/components/InfoSection.vue'
import LatestNewsSection from '~/components/LatestNewsSection.vue'

export default {
  components: {
    Banner,
    IntroSection,
    InfoSection,
    LatestNewsSection,
  },
  computed: {
    latestPost() {
      if (this.posts) return this.posts[0]
      else {
        return null
      }
    },
  },
  async asyncData({ $axios }) {
    const postData = await $axios.$get(
      `http://127.0.0.1/wp/wp-json/wp/v2/posts`
    )
    return { posts: postData }
  },
}
</script>
