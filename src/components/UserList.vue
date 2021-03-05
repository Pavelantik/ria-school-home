<template>
<div>


  <table class="table">
    <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Email</th>
      <th scope="col">Age</th>
    </tr>
    </thead>
    <tbody>
     <tr v-for="(user, index) of userList" :key='user.id'>
       <td>{{index+1}}</td>
       <td>{{user.name | toUpperCase  }}</td>
       <td>{{user.email}}</td>
       <td>{{user.age}}</td>
     </tr>
    </tbody>
  </table>

  
  </div>
</template>

<script>
export default {
name: "UserList",
props: {
  userList: Array
},
filters: {
  toUpperCase: (value) => value.toUpperCase()
}
}
</script>

<style scoped>

</style>