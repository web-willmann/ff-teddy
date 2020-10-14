<template>
  <div>
    <SectionHeading color="blue" noMargin>Aktuelles</SectionHeading>
    <v-container
      class="d-flex align-center justify-center"
      style="height: 300px"
      v-if="isLoading"
    >
        <v-progress-circular
          indeterminate
          color="indigo darken-2"
        ></v-progress-circular>
    </v-container>
    <v-container v-else>
      <v-row>
        <v-col
          v-for="(post, postIndex) in postsOfThisPage"
          :key="postIndex"
          cols="12"
          md="6"
        >
          <v-card>
            <v-img v-if="post._links['wp:featuredmedia']" :src="post._links['wp:featuredmedia'][0].href"></v-img>
            <v-card-title v-html="post.title.rendered"></v-card-title>
            <v-card-text v-html="post.excerpt.rendered"></v-card-text>
            <v-card-actions></v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import SectionHeading from '~/components/SectionHeading.vue'

const postsPerPage = 16

export default {
  components: {
    SectionHeading,
  },
  computed: {
    pageNr: function () {
      return this.$route.params.pageNr
    },
    isLoading: function () {
      let length = 0
      try {
        // Could fail when error data is returned for example.
        length = this.posts.length
      } catch (e) {}
      return length == 0
    },
    postsOfThisPage: function () {
      if (this.isLoading) return []
      return this.posts.slice(
        postsPerPage * (this.pageNr - 1),
        postsPerPage * this.pageNr
      )
    },
  },
  data () {
    return {
      posts: [],
      media: {}
    }
  },
  async fetch() {
    this.posts = await this.$http.$get(`http://127.0.0.1/wp/wp-json/wp/v2/posts?page=1&per_page=${postsPerPage}`)
    // Fetch Preview Images
    this.posts.forEach((post) => {
      if (post._links['wp:featuredmedia']) {
        this.$http.$get(post._links['wp:featuredmedia'][0].href).then((result) => {
          let newMedia = { ...this.media }
          newMedia[post.id] = result
          console.log(newMedia)
          this.$set(this.media, newMedia)
        })
      }
    })
  },
}
</script>