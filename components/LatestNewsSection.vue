<template>
  <div>
    <div class="d-flex flex-column align-end">
      <v-skeleton-loader width="100%" height="200px" type="card">
      </v-skeleton-loader>
      <v-btn class="mt-4 mb-8" color="deep-orange" to="/news"
        >Alle Teddy News</v-btn
      >
    </div>
  </div>
</template>
<script>
export default {
  props: {
    latestPost: Object | null,
  },
}
</script>
