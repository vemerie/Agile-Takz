
    <template>
        <div class="body">
            <nav class="navbar navbar-expand-md navbar-light navbar-laravel">
                <div class="container">
                    <router-link :to="{name: 'home'}" class="navbar-brand">Agile-Takz</router-link>
                    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                        <span class="navbar-toggler-icon"></span>
                    </button>

                    <div class="collapse navbar-collapse" id="navbarSupportedContent">
                        <!-- Left Side Of Navbar -->
                        <ul class="navbar-nav mr-auto"></ul>
                        <!-- Right Side Of Navbar -->
                         <ul class="navbar-nav ml-auto">
        <!-- Authentication Links -->
                            <router-link :to="{ name: 'login' }" class="nav-link" v-if="!isLoggedIn">Login</router-link>
                            <router-link :to="{ name: 'register' }" class="nav-link" v-if="!isLoggedIn">Register</router-link>
                            <li class="nav-link" v-if="isLoggedIn"> Hi, {{name}}</li>
                            <router-link :to="{ name: 'board' }" class="nav-link" v-if="isLoggedIn">Board</router-link>
                            <li class="nav-link" v-if="isLoggedIn" @click="appLogout()">Logout </li>

                        </ul>
                    </div>
                </div>
            </nav>
            <main class="py-4">
                <router-view></router-view>
            </main>
        </div>
    </template>

    <script>
        export default {
        data(){
            return {
                isLoggedIn : null,
                name : null
            }
        },
        mounted(){
            // localStorage.removeItem('jwt')
            this.isLoggedIn = localStorage.getItem('jwt')
            this.name = localStorage.getItem('user')
        },
        methods:{
            appLogout(){
                localStorage.removeItem('jwt')
                this.isLoggedIn=null
            }
        },
    }

    </script>
    <style scoped>
    main{
        background-color: #543;
    }
    .body{
        background-color: #543;
        height:650px;
    }
    </style>
    
