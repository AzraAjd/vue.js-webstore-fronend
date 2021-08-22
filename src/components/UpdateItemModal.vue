<template>
    <div class="updateItem modal">
        <div class="updateItem-inner">
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
                                    <label for="title" class="form-label" value={{item.title}}>Title:</label>
                                    <input class="form-control">
                                </div>
                                <div class="mb-3">
                                    <label for="summary" class="form-label" value="">Description:</label>
                                    <input class="form-control">
                                </div>
                                <div class="mb-3">
                                    <label for="photoURL" class="form-label">Product photo URL:</label>
                                    <input class="form-control">
                                </div>
                                <div class="mb-3">
                                    <label for="price" class="form-label">Price ($):</label>
                                    <input type="number" class="form-control">
                                </div>
                                <div class="mb-3" style="margin:20px">
                                    <button type="button" class="popup-close btn btn-secondary" v-on:click="toggleModal()" style="margin:10px">Close</button>
                                    <button type="submit" class="btn btn-primary" style="margin:10px" v-on:click="submitForm(item.id); toggleModal()">Login</button>
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
        name: 'updateItem',
        props: { item: Object },
        

        /*propsData: {
            type: Object
        }*/
    
        data() {
            return {
                form: {
                    title: '',
                    summary: '',
                    photoURL: '',
                    price: 0
                }
            }
        },
        computed: {
            Article: function() {
                return this.props.propsData
            }
        },
        methods: {
            submitForm(id) {
                let headers = {
                    'Authorization': 'Bearer ' + localStorage.getItem('token')
                };
                axios.post('http://localhost:8080/products/' + id, this.form, { headers })
                    .then((res) => {
                        console.log(res);
                    })
                    .catch((error) => {
                        console.log(error);
                    });
            },
        },
        mounted() {

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