<template>
    <div class="container p-5">
      <h3 class="text-center mt-2 mb-5">therichpost.com</h3>
      <div class="col-md-12">
       
        <form v-on:submit.prevent="create_user">
          <div class="mb-3">
            <label for="exampleFormControlInput1" class="form-label">Enter Name</label>
           <input type="text" name="name" class="form-control" id="exampleInputName1" aria-describedby="nameHelp" placeholder="Enter Username" v-model="form.name">
          </div>
          
         <div class="mb-3">
            <label for="exampleFormControlInput2" class="form-label">Enter Email</label>
           <input type="text" name="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter Email" v-model="form.email">
          </div>

           <div class="mb-3">
            <label for="exampleFormControlInput3" class="form-label">Enter Password</label>
           <input type="password" name="password" class="form-control" id="exampleInputPass1" aria-describedby="passHelp" placeholder="Enter Password" v-model="form.password">
          </div>
      
    
          <button type="submit" class="btn btn-primary mt-5">Submit</button>
    </form>
    </div>
    </div>
</template>

<script>

//importing modules
import "bootstrap/dist/css/bootstrap.min.css";
import axios from 'axios'
import Swal from 'sweetalert2'
export default {
  data(){
  return {
   
    form:{
      name: '',
      email: '',
      password: ''
      
    }
  }
},
  methods:{
     //user register function and api call
     create_user(){
    
      axios
      .post('http://127.0.0.1:8000/api/register',this.form)
      .then((resp) =>{
          //reset form after submission
          this.form.name = '';
          this.form.email = '';
          this.form.password = '';

          //success message alert
          Swal.fire({
          title: 'Hurry',
          text:   "User has been registered successfully",
          icon: 'success',
          
        });
      })
      .catch((e)=>{
          console.log(e); Swal.fire({ title: 'Hurry', text:   e, icon: 'warning', });
      })
    }
  }
  
}
</script>