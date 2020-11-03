<template>
  <div class="study" :id="this.id" v-if="!hide">
    <div class="name" v-if="!editMode">{{name}}  <button class="change-study-name" v-on:click="changeStudyName"> CHANGE NAME </button> </div>
    <td><form v-on:submit="changeStudyName"><input type="text" v-model="name" v-if="editMode" lazy></form></td>
    <div class="id">{{id}}</div>
    <div class="created-date"> {{created}} </div>
    <div class="completes"> {{completes}}<button class="add-complete-button" v-on:click="addComplete"> INCREMENT </button> </div>
    <button class="delete-study-button" v-on:click="hideStudy"> DELETE </button>
  </div>

</template>
<script>
export default {
  name: 'Study',
  props: {
    initialName: String,
    initialId: String,
    initialCreated: String,
    initialCompletes: String
  },
  // props: ['initialName', 'initialId', 'initialCreated', 'initialCompletes'],
// for completes? vvv This may remove the need to use bulky Number and String operations.
// cast value as number??? <input v-model="age" number>


  // computed: {
  //   normalizedCompletes: {
  //     get: function () {
  //       return Number(this.initialCompletes)
  //     },
  //     set: function () {
  //       this.completes += 1;
  //     }
  //   }
  // },
  // computed: {
  //   normalizedCompletes: function() {
  //     return Number(this.initialCompletes);
  //   }
  // },
  // beforeCreate () {
  //   var obj = {}
  //   obj.extend(this.props);
  //   this
  // },

  // Data is currently being refreshed everytime parent reloads causing the changes to not be persisted
  data () {
    return {
      name: this.initialName,
      id: this.initialId,
      created: this.initialCreated,
      completes: this.initialCompletes,
      editMode: false,
      hide: false
      };
  },
  methods: {
    setData: function() {

    },
    //this would be better as a computed value
    addComplete: function() {
      this.completes = String(Number(this.completes) + 1);
    },
    hideStudy: function() {
      this.hide = !this.hide;
    },
    changeStudyName: function() {
      this.editMode = !this.editMode;

    }
  }
}
</script>

<style>
  #Study {
    display: inline-block;
  }
  .study {
    display: flex;
    background-color: #ffffff;
    height: 25px;
    border-radius: 7px;
    margin-bottom: 7px;
    padding: 7px;
  }
  .name {
    width: 45%;
    text-align: left;
    padding-left: 15px;
  }
  .id {
    display: inline-block;
    width: 10%
  }
  .created-date {
    display: inline-block;
    padding-right: 10%;
  }
  .completes {
    display: inline-block;
  }
  .delete-study-button {
    display: inline-block;
  }
  .hide {
    display: none;
  }
</style>