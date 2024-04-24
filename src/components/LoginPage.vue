<template>
<div class="box">
    <img class="logo" src="../assets/resto-logo.jpg" />
    <div class="content">
        <h1>Login</h1>
        <div class="fields">
            <input type="email" v-model="email" placeholder="Enter Your Email" />
            <input type="password" v-model="password" placeholder="Enter Your Password" />
            <button v-on:click="login">Log In</button>
        </div>
        <p>
            <router-link to="/sign-up">Sign Up</router-link>
        </p>
    </div>
</div>
</template>
<script>
import axios from "axios";




export default {
    name: "LoginPage",
    data(){
        return {
            email: "",
            password:"",
        }
    },
    methods: {
        async login(){
            let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`)
            console.log(result);
            
            if (result.status == 200 && result.data.length > 0) {
                localStorage.setItem("user-info", JSON.stringify(result.data[0]))
                this.$router.push({
                    name: 'HomePage'
                })
            }
        }
        
    },
    mounted() {
            let user = localStorage.getItem('user-info')
            if (user) {
                this.$router.push({
                    name: 'HomePage'
                })
            }
        }
}
</script>