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
                            <a v-on:click="DeletedItemAlert(); deleteItem(item.id)" v-if="isAuthenticated == true" href="#" class="btn btn-danger" style="margin-right:15px; color:white">Delete</a>
                            <a v-if="isAuthenticated == true" href="#" class="btn btn-primary" style="margin-right:15px; color:white">Update</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        name: 'hello',
        data() {
            return {
                Article: {},
                isAuthenticated: false
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
            if (localStorage.getItem('token') != null)
                this.isAuthenticated = true;
   
        },
        methods: {
            CheckAuth() {
                if (isAuthenticated = true)
                    location.reload();
            },
            DeletedItemAlert() {
                this.$notify({
                    type: "warn",
                    title: "Item Deleted",
                });
            },
            deleteItem(id) {
                let headers = {
                    'Authorization': 'Bearer ' + localStorage.getItem('token')
                };
                axios.delete('http://localhost:8080/products/' + id, { headers })
                    .then((response) => {
                        console.log(response);
                    });
                location.reload();
            }
        }
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
