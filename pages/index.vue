<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <div class="text-xs-center">
        <svg style="background-color: white" viewBox="0 0 1000 1000" id="straight"></svg>
      </div>
      <v-card>
        <v-card-text id="params">
          <v-text-field clearable label="C1" id="c1" value="0, 0, 255"></v-text-field>
          <v-btn id="emptytBlue" @click.stop="emptytBlue">RND</v-btn>
          <v-btn id="resetBlue" @click.stop="resetBlue">Blue</v-btn>

          <v-text-field label="C1" id="c2" value="255, 235, 59"></v-text-field>
          <v-btn id="emptytYellow" @click.stop="emptytYellow">RND</v-btn>
          <v-btn id="resetYellow" @click.stop="resetYellow">Yellow</v-btn>

          <v-text-field label="C1" id="c3" value="255, 0, 0"></v-text-field>
          <v-btn id="emptytRed" @click.stop="emptytRed">RND</v-btn>
          <v-btn id="resetRed" @click.stop="resetRed">Red</v-btn>

          <v-text-field label="Grid" id="grid" value="41" type="number" steps="1"></v-text-field>
          <input class="input-group--dirty" type="color">
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" flat @click="drawStraight">generate</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  // head: {
  //   title: "Home",
  //   meta: [
  //     {
  //       hid: "description",
  //       name: "description",
  //       content:
  //         "Hi, ich bin Tobias Wust. Ich bin Fullstack Developer und mache Websites und Progressive Webapps mit Vue und Wordpress. Außerdem programmiere ich mit SAP ABAP."
  //     }
  //   ]
  // },
  methods: {
    getColor () {
      const r = Math.round(Math.random() * 255)
      const g = Math.round(Math.random() * 255)
      const b = Math.round(Math.random() * 255)
      return `${r}, ${g}, ${b}`
    },
    drawStraight () {
      document.getElementById('straight').innerHTML = ''
      const grid = document.getElementById('grid').value
      // const grid = 41
      const pixels = 1000 / grid
      const colors = [
        // this.getColor(),
        // this.getColor(),
        // this.getColor()
        document.getElementById('c1').value || this.getColor(),
        document.getElementById('c2').value || this.getColor(),
        document.getElementById('c3').value || this.getColor()
      ]

      console.log(colors)

      for (let i = 0; i <= grid; i += 2) {
        const color = colors[Math.round(Math.random() * 2)]
        for (let j = 0; j <= grid; j += 1) {
          const template = `<rect x="${i * pixels}" y="${j * pixels}" width="${pixels}" height="${pixels}" style="fill:rgb(${color});" />`
          document
            .getElementById('straight')
            .insertAdjacentHTML('beforeend', template)
        }
      }

      for (let i = 1; i <= grid; i += 2) {
        for (let j = 0; j <= grid; j += 2) {
          const color = colors[Math.round(Math.random() * 2)]
          const template = `<rect x="${i * pixels}" y="${j * pixels}" width="${pixels}" height="${pixels}" style="fill:rgb(${color});" />`
          document
            .getElementById('straight')
            .insertAdjacentHTML('beforeend', template)
        }
      }
    },
    resetBlue () {
      document.getElementById('c1').value = '0, 0, 255'
    },
    resetYellow () {
      document.getElementById('c2').value = '255, 235, 59'
    },
    resetRed () {
      document.getElementById('c3').value = '255, 0, 0'
    },
    emptytBlue () {
      document.getElementById('c1').value = ''
    },
    emptytYellow () {
      document.getElementById('c2').value = ''
    },
    emptytRed () {
      document.getElementById('c3').value = ''
    }
  },
  mounted: function () {
    this.drawStraight()
  }
}
</script>

<style scoped>
#params {
  display:grid; grid-template-columns: 1fr 1fr 1fr;
}
</style>