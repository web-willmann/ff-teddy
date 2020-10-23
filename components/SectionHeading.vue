<template>
  <!-- <v-alert
    :color="color"
    :style="noMargin ? 'margin-bottom: 0px' : ''"
    prominent
    tile
  >
    <h5 class="text-h5 text-center white--text">
      <slot></slot>
    </h5>
  </v-alert> -->
  <v-row class="mx-4" justify="center">
      <v-col cols="12" lg="10" xl="8">
        <div class="fancy-font">
          <slot></slot>
        </div>
      </v-col>
  </v-row>
</template>

<script>
export default {
  props: {
    color: String,
    noMargin: {
      type: Boolean,
      default: false,
    },
  },
}
</script>

<style scoped>
.fancy-font {
    font-family: 'Subscriber', sans-serif;
    font-size: 2rem;
}
</style>