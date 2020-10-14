<template>
  <v-alert
    :color="color"
    :style="noMargin ? 'margin-bottom: 0px' : ''"
    prominent
    tile
  >
    <h5 class="text-h5 text-center white--text">
      <slot></slot>
    </h5>
  </v-alert>
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