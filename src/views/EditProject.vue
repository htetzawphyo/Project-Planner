<template>
    <h2 class="mt-5">Project Edit Form</h2>
    <div class="card mt-4">
        <div class="card-body border-0">
            <form @submit.prevent="editProject">
                <div class="mb-3">
                    <label class="small mb-2">TITLE</label>
                    <input type="text" class="form-control" v-model="title">
                </div>
                <div class="mb-3">
                    <label class="small mb-2">DETAIL PROJECT</label>
                    <input type="text" class="form-control" v-model="detail">
                </div>
                <button type="submit" class="btn btn-primary d-flex align-items-center">
                    Update
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
    name: "EditProject",
    props: ["id"],
    data() {
        return {
            title: "",
            detail: ""
        }
    },
    methods: {
        editProject() {
            fetch('http://localhost:3000/projects/'+this.id, {
                method: "PATCH",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(
                    {
                        title: this.title,
                        detail: this.detail
                    }
                )
            })
            .then( () => {
                this.$router.push('/')
            })
            .catch( err => {
                console.log(err)
            })
        }
    },
    mounted() {
        fetch('http://localhost:3000/projects/'+this.id)
        .then( res => {
            return res.json();
        })
        .then( data => {
            this.title = data.title;
            this.detail = data.detail;
        })
        .catch( err => {
            console.log(err)
        })
    }
}
</script>

<style scoped>
    .small {
        font-size: 0.9em;
    }
</style>