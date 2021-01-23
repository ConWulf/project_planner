<template>
  <div class="home">
    <div v-if="projects.length > 0">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="completeProject"/>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from "@/components/SingleProject";

export default {
  name: 'Home',
  components: {
    SingleProject
  },
  data () {
    return {
      projects: []
    }
  },
  mounted () {
    fetch("http://localhost:3000/projects")
    .then(res => res.json())
    .then(data => this.projects = data)
    .catch(console.error)
  },
  methods: {
    handleDelete (id) {
      this.projects = this.projects.filter(elem => elem.id !== id );
    },
    completeProject (id) {
      let p = this.projects.find(project => project.id === id);
      p.complete = !p.complete;
    }
  }
}
</script>