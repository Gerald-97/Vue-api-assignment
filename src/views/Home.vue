<template>
  <div class="workerList">
    <button class="addEntry" @click="addProfile">Create Entry</button>
    <table>
      <thead>
        <tr>
          <th>S/N</th>
          <th>Name</th>
          <th>Salary</th>
          <th>Age</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <WorkerList
          v-for="worker in employeeList"
          :key="worker.id"
          :employee="worker"
          @reloadPage="refreshPage"
        />
      </tbody>
    </table>
  </div>
</template>
<script>

// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import WorkerList from '@/components/employeeProfile.vue'

export default {
  name: 'home',
  components: {
    WorkerList
  },
  data(){
    return {
      employeeList:[]
    }
  },
  mounted(){
    this.refreshPage()
  },
  methods: {
    refreshPage(){
      this.$http.get('http://dummy.restapiexample.com/api/v1/employees')
      .then(response => {
        console.log(response)
        this.employeeList = response.data
      })
      .catch(error => {
        console.log(error.response)
      }) 
    },
    addProfile(){
      this.$router.push({ name: 'new-profile'})
    }
  }
}
</script>
<style scoped>
.workerList{
  width: 80%;
}
.addEntry{
  background-color: beige;
  padding: 10px 25px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  border-radius: 10%;
}
table{
  width: 100%;
  border-collapse: collapse;
  text-align: left;
  margin-top: 1rem;
  border: 2px solid black;
}
th{
  background-color: forestgreen;
  color: #ffffff;
  padding: 1rem;
  font-size: 120%;
  height: 50px;
}
th, td {
  text-align: left;
  border-bottom: 1px solid #ddd;
}

</style>
