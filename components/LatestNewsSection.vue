<template>
  <div>
    <v-row v-if="posts.length > 0">
        <v-col
          v-for="(post, postIndex) in posts"
          :key="postIndex"
          cols="12"
          md="6"
        >
          <v-hover v-slot:default="{ hover }">
            <v-card class="mb-8" :to="`/news/post/${post.id}`" :elevation="hover ? 16 : 2">
                <v-expand-transition>
                  <div
                    v-if="hover"
                    class="d-flex justify-center align-center transition-fast-in-fast-out blue darken-2 v-card--reveal display-3 white--text"
                  >
                    <span class="text-subtitle-2">Klick zum Lesen<v-icon color="blue-grey darken-4" right>mdi-open-in-new</v-icon></span>
                  </div>
                </v-expand-transition>
              <v-img max-height="200px" v-if="mediaExists(post)" :src="mediaOfPost(post).source_url">
              </v-img>
              <v-card-text>{{ formatDate(post.date) }}</v-card-text>
              <v-card-title style="padding-top: 0" v-html="post.title.rendered"></v-card-title>
              <v-card-text v-html="post.excerpt.rendered.slice(0, 120) + '...'" style="margin-bottom: -24px"></v-card-text>
            </v-card>
          </v-hover>
        </v-col>
        <v-col cols="12" md="6">
          <v-hover v-slot:default="{ hover }">
            <v-card class="mb-8" to="/news/1" :elevation="hover ? 16 : 2">
                <v-expand-transition>
                  <div
                    v-if="hover"
                    class="d-flex justify-center align-center transition-fast-in-fast-out blue darken-2 v-card--reveal display-3 white--text"
                  >
                    <span class="text-subtitle-2 text-bold">Klick zum Öffnen</span>
                  </div>
                </v-expand-transition>
              <v-card-text class="d-flex justify-center align-center text-subtitle-1">Mehr News<v-icon right>mdi-open-in-new</v-icon></v-card-text>
            </v-card>
          </v-hover>
        </v-col>
    </v-row>
    <v-row v-else justify="center" align="center">
        <v-progress-circular
          indeterminate
          color="indigo darken-2"
        ></v-progress-circular>
    </v-row>
  </div>
</template>
<script>
import WPAPI from 'wpapi'
import moment from 'moment';
import 'moment/locale/de';

const wp = new WPAPI({ endpoint: process.env.WP_ENDPOINT });

export default {
  props: {
    latestPost: Object | null,
  },
  data () {
    return {
      posts: [],
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
  fetchOnServer: false,
  async fetch() {

    wp.posts().perPage(process.env.postsPerNewsPage).page(this.pageNr).embed().get(( err, data ) => {
      if ( err ) {
          console.log('ERRRO:', err)
      }
      console.log(data)
      this.posts = data.slice(0, 3)
    });

  },
}
</script>
