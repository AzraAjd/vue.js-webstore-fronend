<template>
    <div class="login modal">
        <div class="login-inner">
            <div class="modal" tabindex="-1">
                <div class="modal-dialog">
                    <div class="modal-content">
                        <div class="modal-header">
                            <h5 class="modal-title">Sign In</h5>
                            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                        </div>
                        <div class="modal-body">
                            <form>
                                <div class="mb-3">
                                    <label for="exampleInputEmail1" class="form-label">Email address</label>
                                    <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
                                    <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
                                </div>
                                <div class="mb-3">
                                    <label for="exampleInputPassword1" class="form-label">Password</label>
                                    <input type="password" class="form-control" id="exampleInputPassword1">
                                </div>                             
                                <div class="mb-3" style="margin:20px">
                                    <button type="button" class="popup-close btn btn-secondary" v-on:click="toggleModal()" style="margin:10px">Close</button>
                                    <button type="button" class="btn btn-primary" style="margin:10px">Login</button>
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
    export default {
        name: 'login',
        props: ['toggleModal']
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