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
      <v-btn icon @click.stop="saveImg">
        <v-icon>save</v-icon>
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
      saveImg () {
        saveSvgAsPng.saveSvgAsPng(document.getElementById('straight'), 'straight.png')
      }
    }
  }
</script>
