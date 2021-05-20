<template>
  <div>
    <div class="bouton-reponse u-full-width" v-html="reponse"></div>
    <small v-html="feedback"></small>
  </div>

</template>

<script>
export default {
  name: "boutonReponseQCM",
  props: {
    reponse: String,
    feedback: String
  }
}
</script>

<style scoped>

</style>