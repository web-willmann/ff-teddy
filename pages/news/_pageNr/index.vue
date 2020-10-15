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
          <v-hover>
            <template v-slot:default="{ hover }">
              <v-card>
                <v-img max-height="200px" v-if="mediaExists(post)" :src="mediaOfPost(post).source_url"></v-img>
                <v-card-title v-html="post.title.rendered"></v-card-title>
                <v-card-text v-html="post.excerpt.rendered" style="margin-bottom: -24px"></v-card-text>
                <v-card-text>{{ formatDate(post.date) }}</v-card-text>
                <!-- Overlay when hovered -->
                <v-fade-transition>
                  <v-overlay
                    v-if="hover"
                    absolute
                    color="white"
                  >
                    <v-btn color="blue" :to="'/news/post/' + post.id"><v-icon left>mdi-book-open-variant</v-icon>Lesen</v-btn>
                  </v-overlay>
                </v-fade-transition>
              </v-card>
            </template>
          </v-hover>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import SectionHeading from '~/components/SectionHeading.vue'
import WPAPI from 'wpapi'
import moment from 'moment';
import 'moment/locale/de';

const wp = new WPAPI({ endpoint: process.env.WP_ENDPOINT });

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
    }
  },
  methods: {
    mediaOfPost: function (post) {
      const media = post._embedded['wp:featuredmedia'][0] ?? null
      return media
    },
    mediaExists: function (post) {
      return post._embedded['wp:featuredmedia'] ? true : false
    },
    formatDate: function (date) {
      moment.locale('de')
      return moment(date).format("[Veröffentlicht am] Do MMMM YYYY");
    }
  },
  data () {
    return {
      posts: []
    }
  },
  fetchOnServer: false,
  async fetch() {

    wp.posts().perPage(postsPerPage).page(this.pageNr).embed().get(( err, data ) => {
      if ( err ) {
          console.log('ERRRO:', err)
      }
      console.log(data)
      this.posts = data
    });

  },
}
</script>