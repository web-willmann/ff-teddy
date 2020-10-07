<template>
  <div>
    <v-row no-gutters>
      <v-col><h4 class="text-h4 my-6">Aktuelles</h4></v-col>
      <v-spacer></v-spacer>
      <v-col class="d-flex align-center justify-end"
        ><v-btn text to="/news"
          ><v-icon left>mdi-newspaper</v-icon> Alle News</v-btn
        ></v-col
      >
    </v-row>
    <v-skeleton-loader class="mb-8" width="100%" height="200px" type="card">
    </v-skeleton-loader>
  </div>
</template>
<script>
export default {
  props: {
    latestPost: Object | null,
  },
}
</script>
