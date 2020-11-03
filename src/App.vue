<template>
  <div v-if="this.studies"  id="app">
  <span>is this rendering? {{studies.studyData}}</span>
  <li v-for="study in studies.studyData" :key="study.id">
      <Study :name="study.studyName" :id="study.id" :created="study.creationDate" :completes="study.numCompletes"></Study>
  </li>
  </div>
</template>

<script>
import Study from './components/Study.vue'

export default {
  components: {
    'Study': Study
  },
  name: 'app',
  data () {
    return {
      studies: []
    }
  },
  beforeCreate: function() {
    fetch('https://www.cxsurveys.com/devtest/getStudyData.php')
    .then(res => res.json())
    .then(data => this.studies = data);
    },
  methods: {
    // getStudies: function() {
    //   fetch('https://www.cxsurveys.com/devtest/getStudyData.php')
    //   .then(res => res.json())
    //   .then(data => data);
    // },
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
