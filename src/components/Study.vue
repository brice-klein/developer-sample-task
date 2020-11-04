<template>
  <div class="study" :id="this.id" v-if="!hide">
    <div class="name name-column" v-if="!editMode">
      {{ name }}
      <button class="fas fa-pencil-alt" v-on:click="changeStudyName"></button>
    </div>
    <form class="name-column" v-on:submit="changeStudyName" v-if="editMode">
      <input type="text" v-model="name" class="input-field" />
    </form>
    <div class="id">{{ id }}</div>
    <div class="created-date">{{ created }}</div>
    <div class="completes">
      {{ completes }}
    </div>
    <button class="add-complete-button" v-on:click="addComplete">
      Add Complete
    </button>
    <button class="fas" v-on:click="hideStudy">&#xf2ed;</button>
  </div>
</template>

<script>
export default {
  name: "Study",
  props: {
    initialName: String,
    initialId: String,
    initialCreated: String,
    initialCompletes: String,
  },

  data: function () {
    return {
      name: this.initialName,
      id: this.initialId,
      created: this.getFormattedDate(new Date(this.initialCreated)),
      completes: this.initialCompletes,
      editMode: false,
      hide: false,
    };
  },

  methods: {
    setData: function () {},
    //this would be better as a computed value
    addComplete: function () {
      this.completes = String(Number(this.completes) + 1);
    },
    hideStudy: function () {
      this.hide = !this.hide;
    },
    changeStudyName: function (event) {
      event.preventDefault();
      this.editMode = !this.editMode;
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
#Study {
  display: inline-block;
}
.study {
  display: flex;
  flex-direction: row;
  background-color: #ffffff;
  height: 25px;
  width: 100%;
  border-radius: 8px;
  margin-bottom: 7px;
  padding-left: 25px;
  padding-top: 10px;
  padding-bottom: 10px;
}
.name-column {
  width: 44%;
  text-align: left;
}
.name {
  margin: auto;
  font-weight: bold;
  font-size: 14px;
}
.input-field {
  width: 100%;
  /* display: none; */
}
.id {
  width: 10%;
  display: inline-block;
  margin: auto;
  font-size: small;
}
.created-date {
  width: 21%;
  display: inline-block;
  margin: auto;
  font-size: small;
}
.completes {
  width: 10%;
  display: inline-block;
  margin: auto;
  font-size: small;
}
.add-complete-button {
  background-color: #d4d4d4;
  height: 20px;
  width: 10%;
  /* margin-right: 90px; */
  border: none;
  border-radius: 5px;
  padding: 5px;
  margin: auto;
  color: #396f92;
  box-shadow: 0px 4px 3px rgba(0, 0, 0, 0.2);
}
.fas {
  width: 5%;
  background-color: transparent;
  border: none;
  margin: auto;
  color: gray;
  font-size: 16px;
}
.fas:hover {
  cursor: pointer;
}
.fa-pencil-alt {
  background-color: transparent;
  border: none;
  color: gray;
  height: auto;
  width: auto;
}
.fa-pencil-alt:hover {
  cursor: pointer;
}
.hide {
  display: none;
}
</style>