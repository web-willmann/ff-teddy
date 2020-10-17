<template>
  <v-row class="pa-4" justify="center" no-gutters>
    <v-col class="pr-4" cols="12" md="6" xl="4">
      <h4 class="text-h4 my-6">Frühförderstelle „Teddybär“</h4>
      <p>
        Inmitten des Naturparks Solling liegt der Ort Neuhaus. Hier ist die
        <b>Frühförderstelle „Teddybär“</b> zuhause.
      </p>
      <p>
        Die Einrichtung verfügt über <b>liebevoll</b> eingerichtete und speziell
        auf die kindliche Entwicklung abgestimmte Förderräume. Hier kann je nach
        Bedarf auf viele, teils selbstgefertigte Fördermaterialien
        zurückgegriffen werden. Kinder können somit
        <i>individuell und ganz nach ihren Bedürfnissen</i> und
        Entwicklungsständen gefördert werden.
      </p>
      <p>
        Auch der Außenbereich, von den Mitarbeiterinnen liebevoll „Bullerbü“
        genannt, lädt zum Entdecken und Toben ein. Die Kinder können so
        <b>spielerisch</b> ihre Fähigkeiten entdecken und stärken.
      </p>
      <p>
        Kinder, und auch deren Eltern, fühlen sich hier wohl und kommen gern in
        die Frühförderstelle „Teddybär“.
      </p>
    </v-col>
    <v-col cols="12" md="6" xl="4">
      <v-carousel
        height="400"
        style="border-radius: 6px"
        cycle
        hide-delimiter-background
        show-arrows-on-hover
      >
        <v-carousel-item v-for="(slide, i) in slideshow" :key="i">
          <v-img
            :src="require(`~/assets/slideshow/${slide.file}`)"
            height="100%"
            eager
          >
            <v-chip
              color="white"
              class="ma-2 float-right black--text"
              label
              dense
            >
              <v-icon left>mdi-selection-search</v-icon>
              {{ slide.caption }}
            </v-chip>
          </v-img>
        </v-carousel-item>
      </v-carousel>
    </v-col>
    <!-- <h4 class="text-h4 my-6">Frühförderstelle „Teddybär“</h4>
    <v-card class="px-6 pt-4" elevation="2" tile>
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
            <v-carousel-item>
              <v-img :src="require('~/assets/slideshow/1.jpg')" height="100%">
              </v-img>
            </v-carousel-item>
            <v-carousel-item>
              <v-img :src="require('~/assets/slideshow/2.jpg')" height="100%">
              </v-img>
            </v-carousel-item>
            <v-carousel-item>
              <v-img :src="require('~/assets/slideshow/3.jpg')" height="100%">
              </v-img>
            </v-carousel-item>
            <v-carousel-item>
              <v-img :src="require('~/assets/slideshow/4.jpg')" height="100%">
              </v-img>
            </v-carousel-item>
            <v-carousel-item>
              <v-img :src="require('~/assets/slideshow/5.jpg')" height="100%">
              </v-img>
            </v-carousel-item>
          </v-carousel>
        </v-col> </v-row
    ></v-card> -->
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      slideshow: [
        {
          file: '1.JPG',
          caption: 'Unser Team',
        },
        {
          file: '2.JPG',
          caption: 'Leitspruch',
        },
        {
          file: '3.JPG',
          caption: 'Förderräume',
        },
        {
          file: '4.JPG',
          caption: 'Außenbereich „Bullerbü“',
        },
        {
          file: '5.JPG',
          caption: 'Förderräume',
        },
        {
          file: '6.JPG',
          caption: 'Unser Teddy',
        },
      ],
    }
  },
}
</script>
