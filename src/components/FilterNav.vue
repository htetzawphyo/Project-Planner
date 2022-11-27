<template>
  <div class="filter-nav">
    <button @click="filterBy('all')"  :class="{active: filterValue==='all'}">all</button>
    <button @click="filterBy('complete')"  :class="{active: filterValue==='complete'}">complete</button>
    <button @click="filterBy('ongoing')"  :class="{active: filterValue==='ongoing'}">ongoing</button>
  </div>
</template>

<script>
export default {
    name: "FilterNav",
    props: ["filterValue"],
    methods: {
        filterBy(value){
            this.$emit("filterValue", value)
        }
    }
}
</script>

<style>
    .filter-nav {
        margin-left: 5px;
    }
    .filter-nav button {
        background: none;
        border: none;
        color: #bbb;
        outline: none;
        font-size: 12px;
        text-transform: uppercase;
        margin-right: 10px;
        letter-spacing: 1px;
        font-weight: bold;
        cursor: pointer;
    }
    button.active {
        color: #333;
    }
</style>