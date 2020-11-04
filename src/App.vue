<template>
  <div v-if="this.studies" id="app">
    <div id="header">
      <div class="labels">
        <span id="study-name-header">Study Name</span>
        <span id="study-id-header">Study ID</span>
        <span id="study-created-header">Created</span>
        <span id="study-completes-header">Completes</span>
        <span class="spacer"></span>
      </div>
    </div>
    <div class="studies-container">
      <ul ref="studies">
        <li v-for="study in studies.studyData" :key="study.id">
          <Study
            :initialName="study.studyName"
            :initialId="study.id"
            :initialCreated="study.creationDate"
            :initialCompletes="study.numCompletes"
          ></Study>
        </li>
      </ul>
    </div>
    <br />
    <button id="add-study" v-on:click="createElement">+Add Study</button>
  </div>
</template>

<script>
import Vue from "vue";
import Study from "./components/Study.vue";

var StudyClass = Vue.extend(Study);

export default {
  components: {
    Study: Study,
  },

  name: "app",

  data() {
    return {
      studies: null,
    };
  },

  beforeCreate: function () {
    fetch("https://www.cxsurveys.com/devtest/getStudyData.php")
      .then((res) => res.json())
      .then((data) =>
        this.studies ? (this.studies = this.studies) : (this.studies = data)
      );
  },

  methods: {
    createElement: function () {
      var newStudy = new StudyClass({
        propsData: {
          initialName: "Untitled Study",
          initialId: String(Math.floor(Math.random() * 100000)),
          initialCreated: this.getFormattedDate(new Date()),
          initialCompletes: "0",
        },
      });
      newStudy.$mount();
      this.$refs.studies.appendChild(newStudy.$el);
    },

    getFormattedDate: function (date) {
      var year = date.getFullYear();

      var month = (1 + date.getMonth()).toString();
      month = month.length > 1 ? month : "0" + month;

      var day = date.getDate().toString();
      day = day.length > 1 ? day : "0" + day;

      return month + "/" + day + "/" + year;
    },
  },
};
</script>

<style>
#app {
  background-color: #3d78a3;
  width: 95%;
  height: 100%;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  align-content: center;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#header {
  width: 85%;
  margin-top: 10%;
  padding-top: 10px;
  display: inline-block;
}
.labels {
  display: flex;
  width: 100%;
  padding-left: 25px;
}
#study-name-header {
  width: 44%;
  color: white;
  text-align: left;
  font-size: small;
}
#study-id-header {
  width: 10%;
  color: white;
  font-size: small;
}
#study-created-header {
  width: 21%;
  color: white;
  text-align: center;
  font-size: small;
}
#study-completes-header {
  width: 10%;
  color: white;
  font-size: small;
}
.studies-container {
  width: 85%;
  display: inline-block;
}
.spacer {
  width: 15%;
}
#add-study {
  background-color: #164462;
  height: 25px;
  position: relative;
  right: 42%;
  margin-top: 20px;
  border: none;
  border-radius: 7px;
  color: white;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.2);
}
ul {
  list-style-type: none;
  justify-content: center;
  align-content: center;
  margin-left: none;
  padding-inline-start: 0;
}
</style>
