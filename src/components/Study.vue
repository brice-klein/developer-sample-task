<template>
  <div class="study">
    <div class="name"><div class="change-name-button"> </div> </div>
    <div class="id"> </div>
    <div class="created-date"> </div>
    <div class="completes" ><div class="add-complete-button"> </div> </div>
    <div class="delete-study-button"> </div>
  </div>

<script>
export default {
  name: 'Study',
  props: {
    name: String,
    id: Number,
    created: Date,
    completes: Number
  }
}
</script>

</template>