<template>
<div>
  <span v-html="enonce"></span>
  <div v-for="(reponse, index) in reponses" :key="index" >
    <boutonReponseQCM :reponse="reponse" :feedback="feedbacks[index]"/>
  </div>
  <p><strong>Explication :</strong></p>
  <span v-html="explication"></span>
  <p style="margin-top: 20px;"><strong>Aide :</strong></p>
  <span v-html="aide"></span>
</div>
</template>

<script>
import boutonReponseQCM from "@/components/boutonReponseQCM";

export default {
  name: "afficheQuestion",
  components: {
    boutonReponseQCM
  },
  props : {
    enonce: String,
    reponses: Array,
    feedbacks: Array,
    explication: String,
    aide: String
  },
  updated() {
    // MAJ equations
    // MathJax.typeset();
  }
}
</script>

<style scoped>

</style>