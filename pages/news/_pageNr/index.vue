<template>
  <div style="background-color: #eaeaea; height: 100%;">
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
      <v-row
        v-if="pagination.totalPages > 1"
        align="center"
        justify="center"
      >
          <v-btn v-if="pageNr < 2" disabled icon>
            <v-icon>mdi-chevron-left</v-icon>
          </v-btn>
          <v-btn v-else :to="`/news/${parseInt(pageNr) - 1}`" icon>
            <v-icon>mdi-chevron-left</v-icon>
          </v-btn>
          <div class="text-subtitle-2 text-uppercase">
            Seite <span v-text="pageNr"></span>/<span v-if="pagination" v-text="pagination.totalPages"></span><span v-else>?</span>
          </div>
          <v-btn v-if="pageNr >= pagination.totalPages" disabled icon>
            <v-icon>mdi-chevron-right</v-icon>
          </v-btn>
          <v-btn v-else :to="`/news/${parseInt(pageNr) + 1}`" icon>
            <v-icon>mdi-chevron-right</v-icon>
          </v-btn>
      </v-row>
      <v-row :justify="centerIfOnlyOnePost">
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
              <v-card-text v-html="post.excerpt.rendered" style="margin-bottom: -24px"></v-card-text>
            </v-card>
          </v-hover>
        </v-col>
      </v-row>
      <v-row
        v-if="pagination.totalPages > 1 && posts.length >= 4"
        align="center"
        justify="center"
      >
          <v-btn v-if="pageNr < 2" disabled icon>
            <v-icon>mdi-chevron-left</v-icon>
          </v-btn>
          <v-btn v-else :to="`/news/${parseInt(pageNr) - 1}`" icon>
            <v-icon>mdi-chevron-left</v-icon>
          </v-btn>
          <div class="text-subtitle-2 text-uppercase">
            Seite <span v-text="pageNr"></span>/<span v-if="pagination" v-text="pagination.totalPages"></span><span v-else>?</span>
          </div>
          <v-btn v-if="pageNr >= pagination.totalPages" disabled icon>
            <v-icon>mdi-chevron-right</v-icon>
          </v-btn>
          <v-btn v-else :to="`/news/${parseInt(pageNr) + 1}`" icon>
            <v-icon>mdi-chevron-right</v-icon>
          </v-btn>
      </v-row>
    </v-container>
    <Footer />
  </div>
</template>

<script>
import SectionHeading from '~/components/SectionHeading.vue'
import WPAPI from 'wpapi'
import moment from 'moment';
import 'moment/locale/de';

const wp = new WPAPI({ endpoint: process.env.WP_ENDPOINT });

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
    centerIfOnlyOnePost: function () {
      if (this.posts.length < 2) return "center"
      else return "start"
    },
    pagination: function () {
      return this.posts["_paging"]
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

    wp.posts().perPage(process.env.postsPerNewsPage).page(this.pageNr).embed().get(( err, data ) => {
      if ( err ) {
          console.log('ERRRO:', err)
      }
      console.log(data)
      this.posts = data
    });

  },
}
</script>
