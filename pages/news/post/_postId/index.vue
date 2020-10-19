<template>
  <div style="background-color: #eaeaea; height: 100%">
      <v-container
        class="d-flex align-center justify-center"
        style="height: 100%"
        v-if="loading"
      >
          <v-progress-circular
            indeterminate
            color="indigo darken-2"
          ></v-progress-circular>
      </v-container>
      <v-container v-else >
          <v-row justify="center">
            <v-col cols="12" md="10" lg="8" xl="6">
              <v-card class="pa-6" tile>
                <h1 v-html="post.title.rendered"></h1>
                <v-chip outlined>{{ formatDate(post.date) }}</v-chip>
                <div v-html="post.content.rendered"></div>
              </v-card>
              <v-row justify="center" align="center">
                <v-btn class="mt-4" depressed color="blue-grey white--text" to="/news/1"
                  >Zurück</v-btn
                >
              </v-row>
            </v-col>
          </v-row>
      </v-container>
  </div>
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
.wp-block-embed {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.wp-block-embed * {
  width: 100%;
}
.wp-block-image {
  margin: 10px 0;
  display: flex;
  flex-wrap: nowrap;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #ebebec;
  border-radius: 2px;
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
.wp-block-separator,
.wp-block-embed,
.wp-block-image {
  margin: 15px 0;
}
.wp-block-separator {
  width: 0%;
  min-width: 20%;
  max-width: 100%;
  margin: 20px auto 24px auto;
  border: none;
  border-bottom: 4px solid rgb(42, 45, 51);
  position: relative;
  transition: box-shadow 200ms ease-in-out;
  box-shadow: 0px 0px 0px 0px #f9f9f9;
}
.wp-block-media-text {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
}
</style>