<template>
  <section v-show="loaded" class="container docs-container">
    <h1>{{race.name}}</h1>
    <md-viewer :text="race.desc"/>
    <md-viewer :text="race['asi_desc']"/>
    <md-viewer :text="race['speed_desc']"/>
    <md-viewer :text="race.vision"/>
    <md-viewer :text="race.age"/>
    <md-viewer :text="race.alignment"/>
    <md-viewer :text="race.size"/>
    <md-viewer :text="race.languages"/>
    <md-viewer :text="race.traits"/>

    <h2 v-if="subraceLength > 0">Subraces</h2>
    <div v-for="subrace in race.subraces" v-bind:key="subrace.name">
      <h3>{{subrace.name}}</h3>
      <md-viewer :headerLevel="2" :text="subrace.desc"/>
      <md-viewer :text="subrace['asi_desc']"/>
      <md-viewer :text="subrace.traits"/>
    </div>
  </section>
</template>

<script>
import axios from 'axios'
import MdViewer from '~/components/MdViewer';

export default {
  components:{
    MdViewer
  },
  mounted () {
    return axios.get(`${process.env.apiUrl}/races/${this.$route.params.id}`) //you will need to enable CORS to make this work
    .then(response => {
      this.race = response.data
      this.loaded = true
      this.subraceLength = this.race.subraces.length
    })
  },
  data () {
    return {
      posts: [],
      errors: [],
      race: [],
      loaded: false,
      subraceLength: 0
    }
  },
}
</script>

<style lang="scss">
</style>

