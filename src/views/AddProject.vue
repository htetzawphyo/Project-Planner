<template>
    <h2 class="mt-5">Project Add Form</h2>
    <div class="card mt-4">
        <div class="card-body border-0">
            <form @submit.prevent="addProject">
                <div class="mb-3">
                    <label class="small mb-2">TITLE</label>
                    <input type="text" class="form-control" v-model="title">
                </div>
                <div class="mb-3">
                    <label class="small mb-2">DETAIL PROJECT</label>
                    <input type="text" class="form-control" v-model="detail">
                </div>
                <button type="submit" class="btn btn-primary d-flex align-items-center">
                    Add
                    <span class="material-icons ms-2">
                        save
                    </span>
                </button>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: "AddProject",
    data() {
        return {
            title: "",
            detail: ""
        }
    },
    methods: {
        addProject() {
            fetch('http://localhost:3000/projects', {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(
                    {
                        title: this.title,
                        detail: this.detail,
                        complete: false
                    }
                )
            })
            .then( () => {
                this.$router.push({name:"home"})
            })
            .catch( err => {
                console.log(err)
            })
        }
    }
}
</script>

<style scoped>
    .small {
        font-size: 0.9em;
    }
</style>