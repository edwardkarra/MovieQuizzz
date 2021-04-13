<template>
    <div>
        <b-navbar type="dark" variant="dark">
            <b-navbar-nav class="col-12">
                <b-nav-item active class="col-4">Movie Quizzz</b-nav-item>
                <b-nav-item active class="col-4 offset-4">Score : {{score}}</b-nav-item>
            </b-navbar-nav>
        </b-navbar>
        <br/>
    </div>
</template>
<script>
    export default{
        props:{
            score : Number
        }
    }
</script>
