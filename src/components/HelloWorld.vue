<template v-for="article in Article">
  <div class="hello">
      <div align="center">
          <table class="table">
              <thead>
                  <tr>
                      <th>Title______</th>
                      <th>summary______</th>
                      <th>link______</th>
                      <th>price______</th>
                  </tr>
              </thead>
              <tbody>
                  <tr  v-for="item in Article" :key="item.id">
                      <td>{{item.title}}</td>
                      <td>{{item.summary}}</td>
                      <td>{{item.photoURL}}</td>
                      <td>{{item.price}}</td>
                  </tr>
              </tbody>
          </table>
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
            }
        },
        mounted() {
            axios.get('http://localhost:8080/products/')
                .then((response) => {
                    console.log(response.data);
                    this.Article = response.data;
                })
                .catch((error) => {
                    console.log(error);
                });
  },
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
