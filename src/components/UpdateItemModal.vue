<template>
    <div class="updateItem modal">
        <div class="updateItem-inner">
            <div class="modal" tabindex="-1">
                <div class="modal-dialog">
                    <div class="modal-content">
                        <div class="modal-header">
                            <h5 class="modal-title">Update product</h5>
                            <button v-on:click="toggleModal()" type="button" class="btn-close" aria-label="Close"></button>
                        </div>
                        <div class="modal-body">
                            <form v-on:submit.prevent="submitForm">
                                <div class="mb-3">
                                    <label for="title" class="form-label">Title:</label>
                                    <input class="form-control" v-model="form.title">
                                </div>
                                <div class="mb-3">
                                    <label for="summary" class="form-label" value="">Description:</label>
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
                                    <button v-on:click="toggleModal()" type="button" class="popup-close btn btn-secondary" style="margin:10px">Close</button>
                                    <button v-on:click="submitForm(form.id); toggleModal()" type="submit" class="btn btn-primary" style="margin:10px">Update</button>
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
        props: ['item', 'toggleModal'],

        data() {
            return {
                form: {
                    title: this.item.title,
                    summary: this.item.summary,
                    photoURL: this.item.photoURL,
                    price: this.item.price,
                    id: this.item.id
                }
            }
        },
        watch: {
            item() {
                console.log('item')
            }
        },
        methods: {
            currentData(item) {
                this.form.title = item.title;
                this.form.summary = item.summary;
                this.form.photoURL = item.summary;
                this.form.price = item.summary;
            },
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
                location.reload();
            },
        },
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