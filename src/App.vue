<template>
    <Navbar />
    <HelloWorld />
    <notifications />
    <div id="app">
        <router-view></router-view>
    </div>
</template>

<script>
    import HelloWorld from './components/HelloWorld.vue'
    import Navbar from './components/Navbar.vue'

    export default {
        name: 'App',
        components: {
            Navbar,
            HelloWorld,
        }
}
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 20px;
    }
</style>
