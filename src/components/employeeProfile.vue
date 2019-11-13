<template>
    <tr>
        <td>{{employee.id}}</td>
        <td>{{employee.employee_name}}</td>
        <td>{{employee.employee_salary}}</td>
        <td>{{employee.employee_age}}</td>
        <td class="btn-modify">
            <button @click="deleteRow">Delete Entry</button>
            <button @click="editRow">Edit Entry</button>
        </td>
    </tr>
</template>
<script>
export default {
    name: 'WorkerList',
    props: {
        employee: Object
    },
    methods:{
        deleteRow(){
            this.$http.delete(`http://dummy.restapiexample.com/api/v1/delete/${this.employee.id}`)
            .then(response => {
                alert('Deleted!')
                alert(response)
                this.$emit('reloadPage')
            })
            .catch(error => {
                alert(error.response)
            }) 
        },
        editRow(){
            this.$router.push({ name: 'edit-profile', params: {id: this.employee.id}})
        }
    }
}
</script>
<style scoped>
.btn-modify{
    display: flex;
    justify-content: space-between;
}
.btn-modify > button {
  background-color: rgb(216, 216, 197);
  text-align: center;
  text-decoration: none;
  display: inline-block;
}
tr{
    height: 25px;
    border-bottom: 1px solid #ddd;  
}
tr:hover {
    background-color: beige;
}
tr:nth-child(even){
    background-color: #f2f2f2;
}
td{
    padding: 0.5rem;
}
</style>