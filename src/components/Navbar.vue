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
                        <a class="nav-link disabled" href="#">Add Article</a>
                    </li>
                </ul>
            </li>
            <ul class="nav navbar-nav navbar-right">
                <li class="nav-item" style="float:right">
                    <button class="btn btn-info navlink" type="button">LOGIN</button>
                </li>
            </ul>
        </nav>
     </div>
</template>


<script>
    export default {
        name: 'navbar',
        data() { },
        mounted() {
            console.log("hello");
        }
    }
</script>


<style scoped>

</style>