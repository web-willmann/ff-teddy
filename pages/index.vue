<template>
  <div>
    <HeroBanner />
    <QuoteSection />
    <v-divider />
    <SectionHeading>Unser Angebot</SectionHeading>
    <InfoSection />
    <v-divider />
    <SectionHeading color="blue-grey lighten-2">Aktuelles</SectionHeading>
    <v-container>
      <LatestNewsSection :latestPost="latestPost" />
    </v-container>
    <Footer />
  </div>
</template>

<script>
import Banner from '~/components/Banner.vue'
import HeroBanner from '~/components/HeroBanner.vue'
import InfoSection from '~/components/InfoSection.vue'
import QuoteSection from '~/components/QuoteSection.vue'
import LatestNewsSection from '~/components/LatestNewsSection.vue'
import SectionHeading from '~/components/SectionHeading.vue'

export default {
  components: {
    Banner,
    HeroBanner,
    InfoSection,
    QuoteSection,
    LatestNewsSection,
    SectionHeading,
  },
  computed: {
    latestPost() {
      if (this.posts) return this.posts[0]
      else {
        return null
      }
    },
  },
  data () {
    return {
      posts: [],
    }
  },
  // async asyncData({ $axios }) {
  //   const postData = await $axios.$get(
  //     `http://127.0.0.1/wp/wp-json/wp/v2/posts`
  //   )
  //   return { posts: postData }
  // },
  // fetchOnServer: false,
  // async fetch({ $axios }) {
  //   const posts = await $axios.$get(
  //     `http://127.0.0.1/wp/wp-json/wp/v2/posts`
  //   )
  //   console.log(posts)
  //   this.posts = posts
  // }
}
</script>
