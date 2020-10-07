<template>
  <div>
    <h4 class="text-h4 my-6">Frühförderstelle „Teddybär“</h4>
    <v-card class="px-6 pt-4" elevation="8" tile>
      <v-row>
        <v-col cols="6">
          <p>
            Inmitten des Naturparks Solling liegt der Ort Neuhaus. Hier ist die
            Frühförderstelle „Teddybär“ zuhause.
          </p>
          <p>
            Die Einrichtung verfügt über liebevoll eingerichtete und speziell
            auf die kindliche Entwicklung abgestimmte Förderräume. Hier kann je
            nach Bedarf auf viele, teils selbstgefertigte Fördermaterialien
            zurückgegriffen werden. Kinder können somit individuell und ganz
            nach ihren Bedürfnissen und Entwicklungsständen gefördert werden.
          </p>

          <p>
            Auch der Außenbereich, von den Mitarbeiterinnen liebevoll „Bullerbü“
            genannt, lädt zum Entdecken und Toben ein. Die Kinder können so
            spielerisch ihre Fähigkeiten entdecken und stärken.
          </p>
          <p>
            Kinder, und auch deren Eltern, fühlen sich hier wohl und kommen gern
            in die Frühförderstelle „Teddybär“.
          </p>
        </v-col>
        <v-col cols="6">
          <v-carousel
            cycle
            height="400"
            hide-delimiter-background
            show-arrows-on-hover
          >
            <v-carousel-item v-for="(slide, i) in slides" :key="i">
              <v-sheet :color="colors[i]" height="100%">
                <v-row class="fill-height" align="center" justify="center">
                  <div class="display-3">{{ slide }} Slide</div>
                </v-row>
              </v-sheet>
            </v-carousel-item>
          </v-carousel>
        </v-col>
      </v-row></v-card
    >
  </div>
</template>

<script>
export default {
  data() {
    return {
      colors: [
        'indigo',
        'warning',
        'pink darken-2',
        'red lighten-1',
        'deep-purple accent-4',
      ],
      slides: ['First', 'Second', 'Third', 'Fourth', 'Fifth'],
    }
  },
}
</script>