<template>
  <div class="project" :class="{complete:project.complete}">
    <div class="flexing">
        <div>
            <h3 @click="forShowDetail">{{project.title}}</h3>
            <p v-if="showDetail">{{project.detail}}</p>
        </div>
        <div>
            <span class="material-icons" @click="destroy">
                delete
            </span>
            <router-link :to="{name:'EditProject', params:{id:project.id}}">
                <span class="material-icons edit-link">
                    edit
                </span>
            </router-link>
            <span class="material-icons" @click="completeProject">
            done
            </span>
        </div>
    </div>
  </div>
</template>

<script>
export default {
    name: "SingleProject",
    props: ['project'],
    data() {
        return {
            showDetail: false,
            api: 'http://localhost:3000/projects/'
        }
    },
    methods: {
        forShowDetail() {
            this.showDetail = !this.showDetail
        },
        destroy() {
            let delApi = this.api+this.project.id;
            fetch(delApi, {method: "DELETE"})
            .then( () => {
                this.$emit("delete", this.project.id)
            })
            .catch( err => {
                console.log(err);
            })
        },
        completeProject() {
            let completeApi = this.api+this.project.id;
            fetch( completeApi, {
                method: "PATCH",
                headers: {
                    "Content-Type": "application/json"
                },
                body: JSON.stringify(
                    {complete: !this.project.complete}
                )
            })
            .then( () => {
                this.$emit("complete", this.project.id)
            })
            .catch( err => {
                console.log(err)
            })
        }
    }
}
</script>

<style scoped>
    .project {
        padding: 10px;
        background-color: #eee;
        margin: 10px;
        border-radius: 5px;
        border-left: 4px solid crimson;
    }
    h3 {
        color: indigo;
        cursor: pointer;
    }

    .flexing {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    span {
        cursor: pointer;
        user-select: none;
        margin-left: 10px;
    }
    span:hover {
        color: grey;
    }

    .complete {
        border-left-color: green;
    }

    .edit-link {
        color: #2c3e50;
    }
</style>