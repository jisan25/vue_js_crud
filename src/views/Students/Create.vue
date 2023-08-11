<template>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Add Student</h4>
            </div>
            <div class="card-body">
                <ul class="alert alert-warning" v-if="Object.keys(errorList).length  > 0">
                    <li class="mb-0 ms-3" v-for="(error,index) in errorList" :key="index">
                    {{ error[0] }}
                    </li>
                </ul>
                <div class="mb-3">
                    <label for="">Name</label>
                    <input type="text" class="form-control" v-model="model.student.name">
                </div>
                <div class="mb-3">
                    <label for="">Course</label>
                    <input type="text" class="form-control" v-model="model.student.course">
                </div>
                <div class="mb-3">
                    <label for="">Email</label>
                    <input type="text" class="form-control" v-model="model.student.email">
                </div>
                <div class="mb-3">
                    <label for="">Phone</label>
                    <input type="text" class="form-control" v-model="model.student.phone">
                </div>
                <div class="mb-3">
                    <button @click="saveStudent" type="button" class="btn btn-primary">Save</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default{
    name: 'Create',
    data(){
        return{
            errorList: '',
            model:{
                student:{
                    name:'',
                    course:'',
                    email:'',
                    phone:''

                }
            }
        }
    },
    methods:{
        saveStudent(){
            var mythis = this;
         axios.post('http://127.0.0.1:8000/api/students', this.model.student)
         .then(res=>{
            alert(res.data.message);
            this.model.student = {
                name:'',
                course:'',
                email:'',
                phone:''

            }
            this.errorList = '';
            this.$router.push({name:'students'})
         })
         .catch(function(error){
            if(error.response){
                if(error.response.status == 422){
                    mythis.errorList = error.response.data.errors;
                }
            }
         });
        }
    }
}
</script>