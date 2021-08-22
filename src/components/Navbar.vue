<template>
    <div class="navbar container-fluid" style="margin-bottom:30px">
        <nav class="navbar navbar-expand-xl navbar-light bg-light container-fluid">
            <a class="navbar-brand" href="#">Navbar</a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>

            <li class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav mr-auto">
                    <li class="nav-item active">
                        <a class="nav-link" href="#">Home</a>
                    </li>
                    <li class="nav-item">
                        <a v-if="role != 'ADMIN'" class="nav-link disabled" href="#">Add Item</a>
                        <a v-else-if="role == 'ADMIN'" class="nav-link enabled" href="#" style="color:lightgreen" v-on:click="() => toggleModal('addItemModalTrigger')">Add Item</a>
                        <AddItemModal
                                v-if="modalTriggers.addItemModalTrigger"
                                :toggleModal="() => toggleModal('addItemModalTrigger')">
                        </AddItemModal>
                    </li>
                </ul>
            </li>
            <ul class="nav navbar-nav navbar-right">
                <li class="nav-item" style="float:right">
                    <button v-if="isAuthenticated == false" v-on:click="() => toggleModal('loginModalTrigger')" class="btn btn-info navlink" data-bs-toggle="modal" data-bs-target="#exampleModal" type="button">LOGIN</button>
                    <button v-else v-on:click="LogOut()" class="btn btn-info navlink" data-bs-toggle="modal" data-bs-target="#exampleModal" type="button">LOGOUT</button>
                    <LoginModal @checkAuthentication="CheckAuth($event)"
                                v-if="modalTriggers.loginModalTrigger"
                                :toggleModal="() => toggleModal('loginModalTrigger')">
                    </LoginModal>
                </li>
            </ul>
        </nav>
    </div>
    
</template>


<script>
    import { ref } from 'vue';
    import LoginModal from './LoginModal.vue'
    import AddItemModal from './AddItemModal.vue'
    export default {
        name: 'navbar',
        components: {
            LoginModal,
            AddItemModal
        },
        data() {
            return {
                jwt: localStorage.getItem('token'),
                role: localStorage.getItem('role'),
                isAuthenticated: false,
                isAdmin: true
            }
            
        },
        methods: {
            CheckAuth(auth) {
               if (auth == null)
                   isAuthenticated = false;
                else
                    this.isAuthenticated = true;
            },
            LogOut() {
                localStorage.removeItem('token');
                localStorage.removeItem('role');
                this.isAdmin = false;
                location.reload();
            }
        },
        setup() {
            const modalTriggers = ref({
                loginModalTrigger: false,
                addItemModalTrigger: false
            });

            const toggleModal = (trigger) => {
                modalTriggers.value[trigger] = !modalTriggers.value[trigger]
            };

            return {
                LoginModal,
                AddItemModal,
                modalTriggers,
                toggleModal
            }
        },
        mounted() {
            if (this.jwt != null)
                this.isAuthenticated = true;
        }
    } 
</script>


<style scoped>

</style>