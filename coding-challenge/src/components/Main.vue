<template>
  <div>
    <h3>Online Shopping from Local and International Market</h3>
    <p>Message is: {{ message }}</p>
    <input v-model="message" placeholder="edit me" />
  </div>
    
</template>

<script>
export default {
  name: 'Main',
  // props: {
  //   msg: String
  // }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
