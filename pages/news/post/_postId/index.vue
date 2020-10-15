<template>
    <v-container v-if="!loading">
        <h1 v-html="post.title.rendered"></h1>
        <div v-html="postContent"></div>
    </v-container>
</template>
<script>
import WPAPI from 'wpapi'
import moment from 'moment';
import 'moment/locale/de';

const wp = new WPAPI({ endpoint: process.env.WP_ENDPOINT });

export default {
    computed: {
        postId: function () {
            return this.$route.params.postId
        },
        postContent: function () {
            return this.post?.content?.rendered ?? ''
        }
    },
    data() {
        return {
            post: {},
            loading: true
        }
    },
    fetchOnServer: false,
    async fetch() {

        wp.posts().id( this.postId ).embed().get(( err, data ) => {
        if ( err ) {
            console.log('ERRRO:', err)
        }
        console.log(data)
        this.post = data
        this.loading = false
        });

    },
}
</script>

<style scoped>
@import '~assets/wp_style.css';
/* .wp-block-image {
    display: flex;
    flex-wrap: nowrap;
    justify-content: center;
    align-items: center;
}
.wp-block-image img {
    max-width: 100%;
    max-height: 50vh;
}
.wp-block-separator {
    margin: 20px 0;
}
.wp-block-media-text {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
} */
</style>