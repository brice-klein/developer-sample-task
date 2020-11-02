<template>
  <div v-if="this.studies"  id="app">
  <span>is this rendering?</span>
  <li v-for="study in studies" :key="study.id">
      <div> {{ study.name}} </div>
      <div> {{study.id}} </div>
      <div> {{study.created}} </div>
      <div> {{study.completes}} </div>
  </li>
  </div>
</template>

<script>
//import Study from './components/Study.vue'

export default {
  data () {
    return {
      studies: []
    }
  },
  name: 'app',
  components: {
  },
  mounted: function() {
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
