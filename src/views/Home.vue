<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :currentFilter="current" />
    <div v-if="projects.length > 0">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="completeProject"/>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleProject from "@/components/SingleProject";
import FilterNav from "@/components/FilterNav";

export default {
  name: 'Home',
  components: {
    SingleProject,
    FilterNav
  },
  data () {
    return {
      projects: [],
      current: 'all'
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
  },
  computed: {
    filteredProjects () {
      switch (this.current) {
        case 'complete':
          return this.projects.filter(project => project.complete)
        case 'incomplete':
          return this.projects.filter(project => !project.complete)
        default:
          return this.projects
      }
    }
  }
}
</script>