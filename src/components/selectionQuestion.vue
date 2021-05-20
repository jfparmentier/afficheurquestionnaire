<template>
<div style="margin-top: 3%;" >
  <div class="row">
    <div class="one-half column"><button class="u-full-width" @click="$emit('precedent')" > &lt; </button></div>
    <div class="one-half column"><button class="u-full-width" @click="$emit('suivant')"> &gt; </button></div>
  </div>
</div>
</template>

<script>
export default {
  name: "selectionQuestion",
  props : {
    // nombreQuestions: Number
  },
  data : function() {
    return {
      numeroQuestion: "1"
    }
  },
  emits: ['suivant','precedent']
}
</script>

<style scoped>

</style>