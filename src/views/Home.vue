<template>
    <FilterNav @filterValue="current=$event" :filterValue="current"></FilterNav>
    <div v-for="project in filterProjects" :key="project.id">
        <SingleProject :project="project" @delete="destroy" @complete="completedProject"></SingleProject>
    </div>
</template>

<script>
import FilterNav from '../components/FilterNav'
import SingleProject from '../components/SingleProject'
export default {
  components: {
    FilterNav, 
        SingleProject 
    },
    name: "Home",
    data() {
        return {
            projects: [],
            current: "all"
        }
    },
    methods: {
        destroy(id) {
            this.projects = this.projects.filter( project => {
                return project.id !== id;
            })
        },
        completedProject(id) {
            let findProject = this.projects.find( project => {
                return project.id === id
            })
            findProject.complete = !findProject.complete
        }
    },  
    mounted() {
        fetch("http://localhost:3000/projects")
        .then( response => {
            return response.json();
        })
        .then( datas => {
            this.projects = datas;
        })
        .catch( error => {
            console.log(error);
        })
    },
    computed: {
        filterProjects() {
            if(this.current === "complete"){
                return this.projects.filter( p => {
                    return p.complete;
                })
            }
            if(this.current === "ongoing"){
                return this.projects.filter( p => {
                    return !p.complete;
                })
            }
            return this.projects;
        }
    }
}
</script>

<style>

</style>