<template>
    <nav class="navBar">
        <router-link :to="{name:'home'}" class="navItem">Projects</router-link>
        <router-link :to="{name:'AddProject'}" class="navItem">Add Project</router-link>
    </nav>
</template>

<script>
export default {
    name: "NavBar"
}
</script>

<style>
    .navBar {
        width: 100%;
        font-size: 1.5em;
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 20px 0;
    }
    .navItem {
        color: rgb(65, 61, 61);
        text-decoration: none;
        margin-left: 20px;
        
    }
    .navItem:hover {
        color: indigo;
    }
    .router-link-active {
        border-bottom: 2px solid indigo;
    }
</style>