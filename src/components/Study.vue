<template>
  <div class="study" :id="this.id" v-if="!hide">
    <div class="name" v-if="!editMode">
      {{ name }}
      <button class="fas fa-pencil-alt" v-on:click="changeStudyName"></button>
    </div>
    <td>
      <form v-on:submit="changeStudyName">
        <input type="text" v-model="name" v-if="editMode" class="input-field" />
      </form>
    </td>
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
  // Data is currently being refreshed everytime parent reloads causing the changes to not be persisted
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
  // beforeDestroy: function () {
  //   if (!this.data) {
  //     this.data.id = this.initialId;
  //     this.data.name = this.initialName;
  //     this.data.created = this.initialCreated;
  //     this.data.completes = this.initialCompletes;
  //     this.editMode = false;
  //     this.hide = false;
  //   } else {
  //     this.data = this.data;
  //   }
  // },
  methods: {
    setData: function () {},
    //this would be better as a computed value
    addComplete: function () {
      this.completes = String(Number(this.completes) + 1);
    },
    hideStudy: function () {
      this.hide = !this.hide;
    },
    changeStudyName: function ($event) {
      this.editMode = !this.editMode;
      this.data.name = $event.input;
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
  background-color: #ffffff;
  height: 25px;
  width: 100%;
  border-radius: 8px;
  margin-bottom: 7px;
  padding: 7px;
  padding-top: 13px;
}
.fa {
  background-color: transparent;
  border: none;
  color: gray;
  height: auto;
  width: auto;
}
.fa:hover {
  cursor: pointer;
}
.name {
  width: 43%;
  text-align: left;
  padding-left: 15px;
  font-weight: bold;
}
.input-field {
  width: 422px;
  margin-left: 10px;
}
.id {
  display: inline-block;
  width: 10%;
  font-size: small;
}
.created-date {
  display: inline-block;
  padding-right: 7.5%;
  padding-left: 5.5%;
  font-size: small;
}
.completes {
  display: inline-block;
  font-size: small;
  padding-right: 85px;
  padding-left: 7px;
}
.add-complete-button {
  height: 20px;
  width: auto;
  background-color: #d4d4d4;
  /* margin-right: 90px; */
  border: none;
  border-radius: 5px;
  padding: 5px;
  color: #396f92;
  box-shadow: 0px 4px 3px rgba(0, 0, 0, 0.2);
}
.fas {
  background-color: transparent;
  border: none;
  margin-left: 20px;
  color: gray;
  font-size: 16px;
}
.fas:hover {
  cursor: pointer;
}
.hide {
  display: none;
}
</style>