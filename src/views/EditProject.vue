<template>
  <form @submit.prevent="handleEdit">
    <label>EDIT TITLE</label>
    <input type="text" v-model="title">
    <label>EDIT DESCRIPTION</label>
    <textarea v-model="details"></textarea>
    <button>UPDATE</button>
  </form>
</template>

<script>
export default {
  name: "EditProject",
  props: ['id'],
  data () {
    return {
      title: '',
      details: '',
      uri: `http://localhost:3000/projects/${this.id}`
    }
  },
  mounted () {
    fetch(this.uri)
    .then(res => res.json())
    .then(data => {
      this.title = data.title
      this.details = data.details
    })
  },
  methods: {
    handleEdit () {
      const editedProject = {
        title: this.title,
        details: this.details
      }
      fetch(this.uri, {
        method: "PATCH",
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(editedProject)
      }).then(() => {
        this.$router.push({name: 'Home'})
      }).catch(console.error)
    }
  }
}
</script>
