<template>
    <div>
        <div class="imgcontainer">
            <img src="img_avatar2.png" alt="Avatar" class="avatar">
        </div>

        <div class="container">
            <label for="uname"><b>Email</b></label>
            <input type="text" v-model="email" placeholder="Enter Email" name="uname" required>

            <label for="psw"><b>Password</b></label>
            <input type="password" v-model="password" placeholder="Enter Password" name="psw" required>

            <button @click="login" >Login</button>
            <label>
                <input type="checkbox" checked="checked" name="remember"> Remember me
            </label>
        </div>

        <div class="container" style="background-color:#f1f1f1">
            <button type="button" class="cancelbtn">Cancel</button>
            <span class="psw">Forgot <a href="#">password?</a></span>
        </div>
    </div>
</template>

<script>

import axios from 'axios';
import { response } from 'express';

export default {
    name: "LoginForm",
    data(){
        return{
            // Aquí se registran variables
            email:"",
            password:"",
            //se asigna la variable con v-model
        }
    },

    methods:{
        login: function() {
            var url = 'http://localhost:5211/api/User/SignIn'
            var data = {
                email:this.email,
                password:this.password
            }
            axios.post(url, data)
                .then(response => {
                    console.log("Aquí va la respuesta" + JSON.stringify(response))
                    this.$q.notify({
                        message: "Inicio de Sesión Correcta",
                        color: "positive",
                        position: "bottom",
                        timeout: 3000
                    });
                    this.$router.push("/dashboard")
                }).catch(error => {
                    console.log("Ocurrio un error" + error)
                    this.$q.notify({
                        message: "Ocurrio un error",
                        color: "negative",
                        position: "top",
                        timeout: 3000
                    });
                })
        }
    }
}

</script>

<style>
body {
    font-family: Arial, Helvetica, sans-serif;
    width: 50%;
}

form {
    border: 3px solid #f1f1f1;
}

input[type=text],
input[type=password] {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    box-sizing: border-box;
}

button {
    background-color: #04AA6D;
    color: white;
    padding: 14px 20px;
    margin: 8px 0;
    border: none;
    cursor: pointer;
    width: 100%;
}

button:hover {
    opacity: 0.8;
}

.cancelbtn {
    width: auto;
    padding: 10px 18px;
    background-color: #f44336;
}

.imgcontainer {
    text-align: center;
    margin: 24px 0 12px 0;
}

img.avatar {
    width: 40%;
    border-radius: 50%;
}

.container {
    padding: 16px;
}

span.psw {
    float: right;
    padding-top: 16px;
}

/* Change styles for span and cancel button on extra small screens */
@media screen and (max-width: 300px) {
    span.psw {
        display: block;
        float: none;
    }

    .cancelbtn {
        width: 100%;
    }
}
</style>