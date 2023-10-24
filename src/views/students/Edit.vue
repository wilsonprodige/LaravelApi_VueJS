<template>
  <div class="container mt-5">
    <div class="card">
        <div class="card-header">
            <h4>Edit student</h4>
        </div>
        <div class="card-body">

            <ul class="alert alert-warning" v-if="Object.keys(errorList).length > 0">
                <li class="mb-0 ms-3" v-for="(error,index) in  errorList" :key="index">
                    {{ error[0] }}
                </li>
            </ul>
            <div class="mb-3">
                <label for="name">Name</label>
                <input type="text" class="form-control" v-model="model.student.name">
            </div>
            <div class="mb-3">
                <label for="Course">Course</label>
                <input type="text" class="form-control" v-model="model.student.course">
            </div>
            <div class="mb-3">
                <label for="Email">Email</label>
                <input type="text" class="form-control" v-model="model.student.email">
            </div>
            <div class="mb-3">
                <label for="phone">Phone</label>
                <input type="text" class="form-control" v-model="model.student.phone">
            </div>
            <div class="mb-3">
                <button type="button" @click="updateStudent()" class="btn btn-primary">Save</button>
            </div>


        </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'
export default {
    name:'studentEdit',
    data(){
        return {
            errorList:'',
            model:{
                student:{
                    'name':'',
                    'course':'',
                    'email':'',
                    'phone':''
                }
            },
            studentId:''

        }
    },
    methods:{
        updateStudent(){
            var mythis = this;
            axios.put('http://127.0.0.1:8000/api/students/'+this.studentId+'/edit',this.model.student)
            .then(res=>{
                console.log(res.data);
                alert(res.data.message);
                //empty the fields
                mythis.errorList= '';

            })
            .catch(function(error){
                if (error.response) {

                    if(error.response.status == 422){
                        mythis.errorList = error.response.data.errors;
                    }
                    if(error.response.status == 404){
                       alert(error.response.data.message)
                    }
                  
                   // console.log(error.response.data);
                    //console.log(error.response.status);
                   //console.log(error.response.headers);
                } else if (error.request) {
                 
                    console.log(error.request);
                } else {
                    
                    console.log('Error', error.message);
                }
                //console.log(error.config);
            })
        },
        getStudentData(studentId){
            axios.get('http://127.0.0.1:8000/api/students/'+studentId+'/edit')
            .then(res=>{
                console.log(res.data.student)
                this.model.student.name = res.data.student.name
                this.model.student.course = res.data.student.course
                this.model.student.email = res.data.student.email
                this.model.student.phone = res.data.student.phone

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
    },
    mounted(){
        //console.log(this.$route.params.id);
        this.studentId = this.$route.params.id;
        this.getStudentData(this.$route.params.id);
    }

}
</script>

<style>

</style>