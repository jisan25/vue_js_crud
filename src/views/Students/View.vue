<template>
    <div class="container">
      <div class="card">
        <div class="card-header">
            <h4>students
                <RouterLink to="/student/create" class="btn btn-primary float-end">Add Student</RouterLink>
            </h4>
        </div> <!-- End Card Header-->
        <div class="card-body">
            <table class="table table-bordered">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>Name</th>
                        <th>Course</th>
                        <th>Email</th>
                        <th>Phone</th>
                        <th>Creted At</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody v-if="students.length > 0">
                    <tr v-for="(student, index) in students" :key="index">
                        <td>{{ student.id }}</td>
                        <td>{{ student.name }}</td>
                        <td>{{ student.course }}</td>
                        <td>{{ student.email }}</td>
                        <td>{{ student.phone }}</td>
                        <td>{{ student.created_at }}</td>
                        <td>
                            <RouterLink :to="{path: '/student/edit/'+student.id}" class="btn btn-success me-2">Edit </RouterLink> 
                             <button @click="deleteStudent(student.id)" type="button" class="ml-2 btn btn-danger">Delete</button>
                        </td>
                    </tr>
                </tbody>
                <tbody v-else>
                    <tr class="text-center">
                        <td class="text-success" colspan="7">Loading....</td>
                    </tr>
                </tbody>
            </table>
        </div> <!-- End Card Body -->
      </div>
    </div>
  </template>

  <script>
  import axios from 'axios';
export default{
    name: 'StudentView',
    data(){
        return{
            students:[]
        }
    },
    mounted(){
        this.getStudents();
    },
    methods:{
        getStudents(){
            axios.get('http://127.0.0.1:8000/api/students').then(res=>{
                this.students = res.data.students;
            });
        },
        deleteStudent(id){
            if(confirm('Are you sure?')){
            axios.delete(`http://127.0.0.1:8000/api/students/destroy/${id}`)
            .then(res=>{
               alert(res.data.message);
               this.getStudents();
            })
            .catch(function(error){
            if(error.response){
               
                if(error.response.status == 404){
                    alert(error.response.data.message);
                }
            }
         });  // catch end
        }   
        } 
    }
}
</script>
  