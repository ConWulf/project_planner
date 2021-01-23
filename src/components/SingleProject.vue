<template>
  <div class="project" :class="{complete: project.complete}">
    <div class="actions">
      <h3 @click="viewDetails" >{{project.title}}</h3>
      <div class="icons">
        <router-link :to="{name: 'EditProject', params: {id: project.id}}">
          <span class="material-icons">create</span>
        </router-link>
        <span @click="deleteP" class="material-icons">delete_outline</span>
        <span @click="completed" class="material-icons check">done_outline</span>
      </div>
    </div>
    <div class="details">
      <p v-show="showDetails">{{project.details}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "SingleProject",
  props: ["project"],
  data() {
    return {
      showDetails: false,
      uri: `http://localhost:3000/projects/${this.project.id}`
    }
  },
  methods: {
    viewDetails () {
      this.showDetails = !this.showDetails
    },
    deleteP  () {
      fetch(this.uri, {method: "delete"})
      .then(() => this.$emit("delete", this.project.id))
      .catch(console.error)
    },
    completed () {
      fetch(this.uri, {
        method: "PATCH",
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({complete: !this.project.complete})
      }).then(() => this.$emit("complete", this.project.id))
      .catch(console.error);
    }
  }
}
</script>
