<template>
    <div class="login modal">
        <div class="login-inner">
            <div class="modal" tabindex="-1">
                <div class="modal-dialog">
                    <div class="modal-content">
                        <div class="modal-header">
                            <h5 class="modal-title">Sign In</h5>
                            <button type="button" class="btn-close" v-on:click="toggleModal()" aria-label="Close"></button>
                        </div>
                        <div class="modal-body">
                            <form v-on:submit.prevent="submitForm">
                                <div class="mb-3">
                                    <label for="username" class="form-label">Username</label>
                                    <input class="form-control"  v-model="form.userName">
                                </div>
                                <div class="mb-3">
                                    <label for="exampleInputPassword1" class="form-label">Password</label>
                                    <input type="password" class="form-control" id="exampleInputPassword1" v-model="form.password">
                                </div>                             
                                <div class="mb-3" style="margin:20px">
                                    <button type="button" class="popup-close btn btn-secondary" v-on:click="toggleModal()" style="margin:10px">Close</button>
                                    <button type="submit" class="btn btn-primary" style="margin:10px" v-on:click="submitForm(); toggleModal(); checkIfAdmin()">Login</button>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div> 
</template>

<script>
import axios from "axios"

   
    export default {
        name: 'login',
        props: ['toggleModal'],
        data() {
            return {
                form: {
                    userName: '',
                    password: ''
                },
            }
        },
        methods: {
            submitForm() {
                axios.post('http://localhost:8080/auth', this.form)
                    .then((res) => {
                        console.log(res);
                        this.$emit('checkAuthentication', res.data.jwtToken);
                        localStorage.setItem('token', res.data.jwtToken);   
                        location.reload()
                    })
                    .catch((error) => {
                        console.log(error);
                        this.$emit('checkAuthentication', false)
                    });
            },
            //To-Do parse jwt to get role instead of making another call
            checkIfAdmin() {
                axios.get('http://localhost:8080/users/user/' + this.form.userName )
                    .then((res) => {
                        //console.log(res.data.role);
                        localStorage.setItem('role', res.data.role);
                    })
                    .catch((error) => {
                        console.log(error);
                    });
            },
        }
    }
</script>

<style scoped>
    .modal {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 99;
        background-color: rgba(0, 0, 0, 0.2);
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .login-inner
    {
        background: #FFF;
        padding: 32px;
    }
    
</style>