<template>
  <div class="alert alert-danger" role="alert">        
    <pre>{{message}}</pre>   
  </div>
</template>

<script>
export default {
  name: "Error",
  props: {
    message: String
    }

}
</script>

<style scoped>

</style>