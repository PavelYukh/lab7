<template>
<div class="errors">
  <p>1</p>
  <p v-for="field in errors">{{field}}</p>
</div>
</template>

<script>
export default {
  name: "ErrorField",
  props: ['errors'],

}
</script>

<style scoped>

</style>