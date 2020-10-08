<template>
  <div class="banner background-gradient">
    <v-row align="center" justify="center" style="height: 100%">
      <v-col cols="6" class="quote" align="center" justify="center">
        <!-- <p>{{ quote }} | {{ author }}</p> -->
      </v-col>
    </v-row>
  </div>
</template>
<script>
export default {
  data: function () {
    return {
      quote:
        '„Wenn man genügend spielt, so lange man klein ist, dann trägt man Schätze mit sich herum, aus denen man später sein ganzes Leben lang schöpfen kann‟',
      author: 'Astrid Lindgren',
    }
  },
}
</script>
<style scoped>
.banner {
  height: 400px;
  width: 100%;
}
.background-gradient {
  background: rgb(41, 41, 41);
  background-image: url('~assets/hero-image.jpg');
  background-position: center;
  background-size: cover;
}

.quote,
.author {
  color: white;
  text-shadow: 1px 1px 8px rgba(42, 43, 49, 0.616);
  font-family: 'Tangerine', 'Franklin Gothic Medium', 'Arial Narrow', Arial,
    serif;
}
.quote {
  font-size: 2.5rem;
}
.author {
}
</style>