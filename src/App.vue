
<template>
<div id="tasks-container">
<formtodo/>
<todotasks/>
</div>

</template>

<script>
import formtodo from "./components/formtodo.vue"
import todotasks from "./components/todotasks.vue"
export default{
  name: "App",
  components:{
    formtodo,
    todotasks
  }
}
</script>
<style>
body{
  margin: 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif;
  background-color: rgb(10, 60, 134);
  color: #ffff;
  display: grid;
  justify-items: center;
}
#task-container{
  width: 500px;
    margin-left: auto;
    margin-right: auto;
}
</style>
