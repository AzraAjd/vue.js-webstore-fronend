<template>
    <div class="addItem modal">
        <div class="addItem-inner">
            <div class="modal" tabindex="-1">
                <div class="modal-dialog">
                    <div class="modal-content">
                        <div class="modal-header">
                            <h5 class="modal-title">Add product</h5>
                            <button type="button" class="btn-close" v-on:click="toggleModal()" aria-label="Close"></button>
                        </div>
                        <div class="modal-body">
                            <form v-on:submit.prevent="submitForm">
                                <div class="mb-3">
                                    <label for="title" class="form-label">Title:</label>
                                    <input class="form-control" v-model="form.title">
                                </div>
                                <div class="mb-3">
                                    <label for="summary" class="form-label">Description:</label>
                                    <input class="form-control" v-model="form.summary">
                                </div>
                                <div class="mb-3">
                                    <label for="photoURL" class="form-label">Product photo URL:</label>
                                    <input class="form-control" v-model="form.photoURL">
                                </div>
                                <div class="mb-3">
                                    <label for="price" class="form-label">Price ($):</label>
                                    <input type="number" class="form-control" v-model="form.price">
                                </div>
                                <div class="mb-3" style="margin:20px">
                                    <button type="button" class="popup-close btn btn-secondary" v-on:click="toggleModal()" style="margin:10px">Close</button>
                                    <button type="submit" class="btn btn-primary" style="margin:10px" v-on:click="submitForm(); toggleModal()">Login</button>
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
        name: 'addItem',
        props: ['toggleModal'],
        data() {
            return {
                form: {
                    title: '',
                    summary: '',
                    photoURL: '',
                    price: 0
                },
            }
        },
        methods: {
            submitForm() {
                let headers = {
                    'Authorization': 'Bearer ' + localStorage.getItem('token')
                };
                axios.post('http://localhost:8080/products', this.form, { headers })
                    .then((res) => {
                        console.log(res);
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

    .login-inner {
        background: #FFF;
        padding: 32px;
    }
</style>