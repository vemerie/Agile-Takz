<template>
        <div class="container">
            <div class="row justify-content-center">
                <div class="col-md-5">
                    <div class="card card-default">
                        <div class="card-header">Login</div>

                        <div class="card-body">
                            <form method="POST" action="/login">
                                <div class="form-group row">
                                    <!-- <label for="email" class="col-sm-4 col-form-label text-md-right">E-Mail Address</label> -->

                                    <div class="col-md-10 offset-md-1">
                                        <input id="email"  placeholder="Email" type="email" class="form-control" v-model="email" required autofocus>
                                    </div>
                                </div>

                                <div class="form-group row">
                                    <!-- <label for="password" class="col-md-4 col-form-label text-md-right">Password</label> -->

                                    <div class="col-md-10 offset-md-1">
                                        <input id="password" placeholder="password" type="password" class="form-control" v-model="password" required>
                                    </div>
                                </div>

                                <div class="form-group row mb-0">
                                    <div class="col-md-8 offset-md-2">
                                        <button type="submit" class="btn btn-primary btn-lg" @click="handleSubmit">
                                            Login
                                        </button>
                                    </div>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </template>

    <script>
        export default {
            data(){
                return {
                    email : "",
                    password : ""
                }
            },
            methods : {
                handleSubmit(e){
                    e.preventDefault()

                    if (this.password.length > 0) {
                        axios.post('api/login', {
                            email: this.email,
                            password: this.password
                          })
                          .then(response => {
                            localStorage.setItem('user',response.data.success.name)
                            localStorage.setItem('jwt',response.data.success.token)

                            if (localStorage.getItem('jwt') != null){
                                this.$router.go('/board')
                            }
                          })
                          .catch(function (error) {
                            console.error(error);
                          });
                    }
                }
            },
            beforeRouteEnter (to, from, next) { 
                if (localStorage.getItem('jwt')) {
                    return next('board');
                }

                next();
            }
        }
    </script>
    <style scoped>
    .container{
        margin-top: 40px;
    }
.card-header{
        font-size: 16px;
        font-weight: bold;
        color: #543;
    }

    button{
        background-color: #543;
        border-radius: unset;
        width:100%;
         font-size:16px;
    }
    
    button:hover{
        background-color: white;
        border-radius:unset ;
        width:100%;
        color:#543;
        border: 1px solid #543;
        font-size: 16px;

    }
    input{
        height:50px;
        border-radius:unset;
    }
    </style>
    