<template v-for="article in Article">
    <div class="hello">
        <div class="container">
            <div class="row">
                <div class="col" v-for="item in Article" :key="item.id">
                    <div class="card">
                        <div class="top-img-container">
                            <img class="card-img-top" v-bind:src="item.photoURL" alt="" style="" />
                        </div>
                        <div class="card-body">
                            <h5 class="card-title" style="max-height: 50px;">{{item.title}}</h5>
                            <hr>
                            <p class="card-text" style="height:70px; width:310px;">{{item.summary}}</p>
                            <p class="card-text">{{item.price}}$</p>
                            <a v-if="role == 'ADMIN'" v-on:click="deleteItem(item.id)" href="#" class="btn btn-danger" style="margin-right:15px; color:white">Delete</a> <!--reloading page removes toast message-->
                            <a v-if="role == 'ADMIN'" v-on:click="toggleModal(); selectItem(item)" href="#" class="btn btn-primary" style="margin-right:15px; color:white">Update</a>
                            <UpdateItemModal v-if="modalTrigger" 
                                             v-bind:item="selectedItem"
                                             :toggleModal="() => toggleModal()"
                                             :currentData="() => currentData(item)">
                            </UpdateItemModal>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import UpdateItemModal from './UpdateItemModal.vue';
    export default {
        name: 'hello',
        components: { UpdateItemModal },
        data() {
            return {
                Article: {},
                isAuthenticated: false,
                isAdmin: false,
                role: "",
                modalTrigger: false,
                selectedItem: {}
            }
        },
        mounted() {
            axios.get('http://localhost:8080/products')
                .then((response) => {
                    console.log(response.data);
                    this.Article = response.data;
                })
                .catch((error) => {
                    console.log(error);
                });
            this.role = localStorage.getItem('role');
        },
        methods: {
            selectItem(item) {
                this.selectedItem = item;
            },
            unselectItem(item) {
                this.selectedItem = {};
            },
            toggleModal() {
                this.modalTrigger = !this.modalTrigger;
            },
            CheckAuth() {
                if (isAuthenticated = true)
                    location.reload();
            },
            deleteItem(id) {
                console.log(id)
                let headers = {
                    'Authorization': 'Bearer ' + localStorage.getItem('token')
                };
                axios.delete('http://localhost:8080/products/' + id, { headers })
                    .then((response) => {
                        console.log(response);
                        location.reload();
                    })
                    .catch((error) => {
                        console.log(error);
                    });
            }
        }
       /*setup() {
           const modalTriggers = ref({
               loginModalTrigger: false,
               addItemModalTrigger: false,
                updateModalTrigger: false
            });

            const toggleModal = (trigger) => {
                modalTriggers.value[trigger] = !modalTriggers.value[trigger]
            };

           return {
                LoginModal,
                AddItemModal,
                UpdateItemModal,
                updateModalTrigger,
                modalTriggers,
                toggleModal
            }
        }*/
}
</script>



<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
