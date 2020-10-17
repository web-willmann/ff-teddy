<template>
  <v-container v-if="!loading" style="background-color: #eaeaea">
    <v-row justify="center">
      <v-col cols="12" md="10" lg="8" xl="6">
        <v-card class="pa-6" tile>
          <h1 v-html="post.title.rendered"></h1>
          <v-chip outlined>{{ formatDate(post.date) }}</v-chip>
          <div v-html="post.content.rendered"></div>
        </v-card>
        <v-row justify="center" align="center">
          <v-btn class="mt-4" color="blue white--text" to="/news/1"
            >Zurück</v-btn
          >
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import WPAPI from 'wpapi'
import moment from 'moment'
import 'moment/locale/de'

const wp = new WPAPI({ endpoint: process.env.WP_ENDPOINT })

export default {
  computed: {
    postId: function () {
      return this.$route.params.postId
    },
  },
  data() {
    return {
      post: {},
      loading: true,
    }
  },
  fetchOnServer: false,
  async fetch() {
    wp.posts()
      .id(this.postId)
      .embed()
      .get((err, data) => {
        if (err) {
          console.log('ERRRO:', err)
        }
        console.log(data)
        this.post = data
        this.loading = false
      })
  },
  methods: {
    formatDate: function (date) {
      moment.locale('de')
      return moment(date).format('[Veröffentlicht am] Do MMMM YYYY')
    },
  },
}
</script>

<style lang="scss">
// @import '~assets/wp_style.scss';
.wp-block-image {
  margin: 10px 0;
  display: flex;
  flex-wrap: nowrap;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
}
figcaption {
  opacity: 0.6;
}
.wp-block-image img {
  max-width: 100%;
  max-height: 50vh;
}
h1,
h2,
h3,
h4,
h5,
h6,
p,
ul,
ol,
.wp-block-separator {
  margin: 10px 0;
}
.wp-block-media-text {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
}
</style>