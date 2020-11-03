<template>
  <div class="study">
    <div class="name">{{name}}<div class="change-name-button"> </div> </div>
    <div class="id">{{id}}</div>
    <div class="created-date"> {{created}} </div>
    <div class="completes" > {{completes}}<div class="add-complete-button"> </div> </div>
    <div class="delete-study-button"> </div>
  </div>

</template>

<script>
export default {
  name: 'Study',
  data () {
    return {studies: []};
  },
  props: {
    name: String,
    id: String,
    created: String,
    completes: String
  }
}
</script>