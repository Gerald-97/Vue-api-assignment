<template>
    <div class="form">
        <h1>New Entry</h1>
        <form class="newProfile" v-on:submit.prevent="newProfile">
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
            <button type="submit">Add Profile</button>
        </form>
    </div>
</template>
<script>
export default {
    name:'EditForm',
    data(){
        return{
            employee: {
                employee_name: '',
                employee_salary: '',
                employee_age: ''
            }
        }
    },
    methods: {
        newProfile(){
            this.$http.post('http://dummy.restapiexample.com/api/v1/create', this.employee)
            .then(response =>{
                this.employee = {
                    employee_name: '',
                    employee_salary: '',
                    employee_age: ''
                }
                alert('New Profile created!')
                alert(response)
            })
            .catch(error => {
                alert(error.response)
            })
        }
    }
}
</script>
<style scoped>
.newProfile{
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