<template>
  <div v-if="this.studies"  id="app">
    <div id="header">
      <span id="study-name-header">Study Name</span>
      <span id="study-id-header">Study ID</span>
      <span id="study-created-header">Created</span>
      <span id="study-completes-header">Completes</span>
    </div>
    <div class="studies">
      <ul>
        <li v-for="study in studies.studyData" :key="study.id">
          <Study :initialName="study.studyName" :initialId="study.id" :initialCreated="study.creationDate" :initialCompletes="study.numCompletes"></Study>
        </li>
      </ul>
    </div>
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
  }
}
</script>

<style>
#app {
  background-color: #2c6992;
  width: 100%;
  height: 100%;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#header {
  width: 100%;
  margin-top: 10%;
  display: flex;
}
#study-name-header {
  width: 24%;
  color: white;
  text-align: left;
  margin-left: 15%;
}
#study-id-header {
  width: 10%;
  color: white;
}
#study-created-header {
  width: 10%;
  padding-right: 10%;
  color: white;
  text-align: left;
}
#study-completes-header {
  width: auto;
  color: white;
}
.studies {
  width: 80%;
  display: inline-block;
}
ul {
  list-style-type: none;
}
li {
  width: 80%
}
</style>
