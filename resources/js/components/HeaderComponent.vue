<template>
   <div class="p-3">
    <nav class="navbar navbar-expand-lg navbar-light bg-light py-3">
        <a class="navbar-brand" href="#">SHOP CART</a>

        <ul class="nav ml-auto">
            <li class="nav-item px-3  dropdown">
              <a href="#" class="nav-link" id="navbarDropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                <i class="fa fa-shopping-cart fa-lg text-dark"></i> 
                <span class="itm" v-if="cart.length > 0">{{cart.length}}</span>
                </a>
                 <div class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink" v-if="cart.length > 0">
                     <div v-for="item in cart" :key="item.id">
                            <a class="dropdown-item" href="#">{{item.name}}</a> 
                            <!-- <span><i class="fa fa-trash fa-lg text-dark"></i></span> -->
                            <hr>
                     </div>
                    <a class="btn btn-primary mx-1 w-100" href="#">Check Out</a>
                </div>
            </li>
            <li class="nav-item px-3">
              <a href="#" class="nav-link" data-toggle="modal" data-target="#login">
                <i class="fa fa-user fa-lg text-dark" ></i> 
                </a>
            </li>
        </ul>
    </nav>

    <!-- Modal -->
<div class="modal fade" id="login" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">Login</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
      <div class="modal-body">
          <form>
            <div class="form-group">
                <label for="exampleInputEmail1">Email address</label>
                <input v-model="email" type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email">
                <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
            </div>
            <div class="form-group">
                <label for="exampleInputPassword1">Password</label>
                <input v-model="password" type="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
            </div>
            <div class="form-check">
                <label class="form-check-label">
                <input type="checkbox" class="form-check-input">
                Check me out
                </label>
            </div>
            <button type="submit" class="btn btn-primary" @click="login()">Submit</button>
        </form>
      </div>
    </div>
  </div>
</div>
</div>
</template>

<script>
    export default {
       props:['cart'],
       data(){
           return{
               email: '',
               password: ''
           }
       },
       methods:{
           login(){
               axios.post(`/login`)
                    .then((res)=>{
                        localStorage.setItem('user', res.data.user)
                    })
           }
       }
    }
</script>

<style >
.itm {
    position: absolute;
    top: -5%;
    right: 18px;
    font-size: 18px;
    font-weight: bold;
    color: black;
}

</style>


