<template>
  <div>
    <div class="layout-view">
      <div class="text-center">
        <h1>Bow Chicka Wow Wow</h1>
      </div>
      <div class="layout-padding text-center">
        <q-card inline v-for="doge in doges" :key="doge.id">
          <!-- Todo: A doge should be its own component -->
          <a :href="'#/doges/' + doge.id">
            <div class="text-center doge-pic-wrapper">
              <img alt="doge image" :title="doge.name" :src="doge.image" class="doge-pic">
            </div>
          </a>
          <q-card-separator />
          <q-card-title>
            <a :href="'#/doges/' + doge.id">{{ doge.name }}</a>
            <q-checkbox
              slot = "subtitle"
              v-model = "checked"
              checked-icon = "pets"
              unchecked-icon = "pets"
              :label = "doge.liked_count"
              @click="adjustLikes"
            />
            <div slot="right" class="row items-center">
              <a href="#" class="pop"><b>Adopt</b></a> <q-icon name="swap calls" /> 0.0032
            </div>
          </q-card-title>
          <q-card-separator />
          <q-card-main>
            <img class="gene-icon" alt="double helix" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAGbSURBVFhH7dZNK0RRHMfxIZQF3oCFlaJkwdIGSSRFsvMOkBKRiLJiRbFSVjbegawUL0CJPCyQN0BRytP3e5tbspk5985kFvOrTzlH53/uveeeMzdTTjmlnBd8oy5qJUstrPEatQJzBQe3RK1kaYM1bqNWYA7g4Gn0Z/9OylrBGYGDz1GFo2w7iXEEpxrXsMCkHYFZgmN9/N5AogzgC+/osSPPDOMDju2zI03W4Z34Jg+hCWfZvlxWkToV2IIFvatl1GAt2/47aWwTBY3vQTzhKX5vz0Ycw/+5XFMoSlzPR8QT+Yh9GhtwvW/QiaKmAfuIH/UlutCBNKdm3qnHHuIL0Cd24cUVNW7FezjpG+axApfDvid0o+BxJ7jerrMTnaAZcVoRb01f1EUULJWI19ziC/CUzLUNd+CFp842LOhBNIiQg8hDLFXGYCHXuNeOPON29em4ZB7nieL+foAXMGtHYObgWM8Glyw4E7DABSyQ5ud4FME5hINn8C8fJHdwcJpPsnZYw8+74PjWOzjN8erJaI3nqFVOOaWXTOYHPHK+Rva+tQEAAAAASUVORK5CYII=">
            <h6>Genes</h6>
            <q-card-separator />
              <q-chip v-for="gene in doge.genes" :key="gene.id" small tag color="black">
                <a href="#">
                  {{ gene }}
                </a>
              </q-chip>
          </q-card-main>
        </q-card>
      </div>
    </div>
  </div>
</template>

<style scoped>
.q-card {
  width: 300px;
}
.q-card:hover {
  transform: scale(1.05) rotateZ(-2deg);
  transition: all .4s ease-in-out;
}
.q-card a {
  color: black;
}
.doge-pic-wrapper {
  padding: 30px;
}
.doge-pic {
  max-height: 100px;
}
.q-card-main .gene-icon {
  float: left;
}
.q-card-main h6 {
  text-align: left;
}
.q-chip {
  margin: 5px 5px 0 0;
}
.q-chip-main a {
  color: white;
}
.q-chip:hover {
  transform: scale(1.05);
  transition: all .1s ease-in-out;
  cursor: pointer;
}
.pop:hover {
  transform: scale(1.1);
  transition: all .1s ease-in-out;
}
</style>

<script>
  import { Toast, QCard, QCardTitle, QCardSeparator, QCardMain, QIcon, QCheckbox, QChip } from 'quasar'
  import axios from 'axios'
  import menu from '../layouts/menu'

  export default{
    data () {
      return {
        doges: {},
        checked: false
      }
    },

    mounted () {
      this.fetchDoges()
    },

    methods: {
      fetchDoges () {
        axios.get('doges')
          .then((response) => {
            this.doges = response.data.data
          }, () => {
            Toast.create.negative('Something went wrong!')
          })
      },

      adjustLikes () {
        console.log('test')
      }
    },

    components: { 'q-menu': menu, Toast, QCard, QCardTitle, QCardSeparator, QCardMain, QIcon, QCheckbox, QChip }
  }
</script>
