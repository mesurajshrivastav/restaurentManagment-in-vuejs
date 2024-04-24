<template>
<div class="box">
    <img class="logo" src="../assets/resto-logo.jpg" />
    <div class="content">
        <h1>Registration</h1>
        <div class="fields">
            <input type="text" v-model="name" placeholder="Enter Your Name" />
            <input type="email" v-model="email" placeholder="Enter Your Email" />
            <input type="password" v-model="password" placeholder="Enter Your Password" />
            <button v-on:click="getData()">Sign Up</button>
        </div>
        <p>
            <router-link to="/log-in">Login</router-link>
        </p>
    </div>
</div>
</template>

<script>
import axios from "axios";

export default {
    name: "SignUp",
    data() {
        return {
            name: "",
            email: "",
            password: "",
        };
    },
    methods: {
        async getData() {
            let result = await axios.post("http://localhost:3000/users", {
                name: this.name,
                email: this.email,
                password: this.password,
            });

            if (result.status == 201) {
                localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({
                    name: 'HomePage'
                })
            }

        },
    },
    mounted() {
            let user = localStorage.getItem('user-info')
            if (user) {
                this.$router.push({
                    name: 'HomePage'
                })
            }
        }
};
</script>

<style>

</style>
