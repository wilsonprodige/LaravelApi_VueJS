<template>
    <div class="container">
        <div class="card">
            <div class="card-header">
                <h4>
                    Student
                    <RouterLink to="/students/create" class="btn btn-primary float-end">Add Student</RouterLink>
                </h4>
            </div>
            <div class="card-body">
                <table class="table table-bordered">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>NAME</th>
                            <th>EMAIL</th>
                            <th>PHONE</th>
                            <th>COURSE</th>
                            <th>CreatedAt</th>
                            <th>ACTION</th>
                        </tr>
                    </thead>
                    <tbody v-if="students.length > 0">
                        <tr v-for="(student, index) in students" :key="index">
                            <td>{{ student.id }}</td>
                            <td>{{ student.name }}</td>
                            <td>{{ student.email }}</td>
                            <td>{{ student.phone }}</td>
                            <td>{{ student.course }}</td>
                            <td>{{ student.created_at }}</td>
                            <td>
                                <RouterLink :to="{path:'/students/'+student.id+'/edit'}" class="btn btn-success mx-1">
                                    Edit
                                </RouterLink>
                                <button @click="destroyStudent(student.id)" type="button" class="btn btn-danger">Delete</button>


                            </td>


                        </tr>
                    </tbody>
                    <tbody v-else>
                        <td colspan="7">Loading...</td>
                    </tbody>

                </table>
            </div>
        </div>
    </div>
  
</template>

<script>
import axios from 'axios';

export default {
    name:'StudentsView',
    data(){
        return {
            students:[],
        }
    },
    mounted(){
        console.log('I am here');
        this.getStudents()
    },
    methods:{
        //getting student list from api
        getStudents(){
            axios.get('http://127.0.0.1:8000/api/students')
            .then(res=>{
                this.students = res.data.students
                console.log(this.students)

            })
            .catch(err=>{
                console.log(err)
            })

        },
        destroyStudent(id){
           

            if(confirm('Are you sure you want to delete this data?')){
               // console.log(id);
                axios.delete('http://127.0.0.1:8000/api/students/'+id+'/delete')
                .then(res=>{
                   alert(res.data.message)
                   //location.reload(true)
                   this.getStudents()
                })
                .catch(function(error){
                if (error.response) {

                    if(error.response.status == 404){
                        alert(error.response.data.message)
                    }
                  
                   // console.log(error.response.data);
                    //console.log(error.response.status);
                   //console.log(error.response.headers);
                } else {
                    
                    console.log('Error', error.message);
                }
                //console.log(error.config);
            })

            }
            
        }

    }

}
</script>

<style>

</style>