<template>
  <div class="study">
    <div class="name">{{initialName}} </div>
    <div class="id">{{initialId}}</div>
    <div class="created-date"> {{initialCreated}} </div>
    <div class="completes"> {{completes}}<button class="add-complete-button" v-on:click="completes += 1"> </button> </div>
    <div class="delete-study-button"> </div>
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
  data () {
    return {
      name: this.initialName,
      id: this.initialId,
      created: this.initialCreated,
      completes: this.initialCompletes
      };
  },
  methods: {
    addComplete: function() {
      this.completes = this.completes + 1;
    }
  }
}
</script>