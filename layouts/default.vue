<template>
  <v-app dark>
    <v-navigation-drawer
      :mini-variant.sync="miniVariant"
      :clipped="clipped"
      v-model="drawer"
      fixed
      app
    >
      <v-list>
        <v-list-tile
          router
          :to="item.to"
          :key="i"
          v-for="(item, i) in items"
          exact
        >
          <v-list-tile-action>
            <v-icon v-html="item.icon"></v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title"></v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar fixed app :clipped-left="clipped">
      <v-toolbar-side-icon @click="drawer = !drawer"></v-toolbar-side-icon>
      <v-btn flat @click.stop="savePng">
        <v-icon>save</v-icon>
        <span>PNG</span>
      </v-btn>
      <v-btn flat @click.stop="saveSvg">
        <v-icon>save</v-icon>
        <span>SVG</span>
      </v-btn>
    </v-toolbar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer :fixed="fixed" app>
      <span>&copy; {{ new Date().getFullYear() }} <a href="https://www.tobiaswust.de">Tobias Wust</a></span>
    </v-footer>
  </v-app>
</template>

<script>
  import saveSvgAsPng from 'save-svg-as-png'
  import saveAs from 'file-saver'

  export default {
    data () {
      return {
        clipped: true,
        drawer: false,
        fixed: true,
        items: [
          { icon: 'apps', title: 'Generate', to: '/' },
          { icon: 'bubble_chart', title: 'About', to: '/about' }
        ],
        miniVariant: false,
        right: true,
        rightDrawer: false,
        title: 'Palermo Generator'
      }
    },
    methods: {
      savePng () {
        saveSvgAsPng.saveSvgAsPng(document.getElementById('straight'), 'straight.png')
      },
      saveSvg () {
        var text = document.getElementById('straight').outerHTML
        var blob = new Blob([text], { type: 'image/svg+xml' })
        saveAs(blob, 'straight.svg')
      }
    }
  }
</script>
