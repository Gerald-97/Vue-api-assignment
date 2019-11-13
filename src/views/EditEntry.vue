<template>
<div class="container">
    <h1>Update Entry</h1>
    <form class="employee" v-on:submit.prevent="updateProfile">
        <div class="form__item">
            <label for="name">Name</label>
            <input type="name" v-model="employee.employee_name">
        </div>
        <div class="form__item">
            <label for="salary">Salary</label>
            <input type="number" v-model="employee.employee_salary">
        </div>
        <div class="form__item">
            <label for="age">Age</label>
            <input type="number" v-model="employee.employee_age">
        </div>
        <button type="submit">Update Profile</button>
    </form>
</div>
</template>
<script>
export default {
    name:'edit-profile',
    data(){
        return{
            employee: {
                employee_name: '',
                employee_salary: '',
                employee_age: ''
            }
        }
    },
    mounted(){
        this.$http
        .get(
            `http://dummy.restapiexample.com/api/v1/employee/${this.$route.params.id}`
        )
        .then(response => {
            this.employee = response.data
            console.log(response)
        })
        .catch(error => {
            alert(error.response)
        })
    },
    methods: {
        updateProfile(){
            this.$http
            .put(
                `http://dummy.restapiexample.com/api/v1/update/${this.$route.params.id}`, 
                this.employee
            )
            .then(response =>{
                alert(`Updated Profile with id ${response.data.id}`)
                this.employee = {
                    employee_name: '',
                    employee_salary: '',
                    employee_age: ''
                }
            })
            .catch(error => {
                alert(error.response)
            })
        }
    }
}
</script>
<style scoped>
.employee{
    border: 2px solid #ddd;
    display: flex;
}
button {
  background-color: rgb(216, 216, 197);
  text-align: center;
  text-decoration: none;
  display: inline-block;
}
.form__item{
    padding: 0.5rem;
}
.form__item > label{
    padding-right: 20px;
}
.form__item > input{
    height: 20px;
}
</style>