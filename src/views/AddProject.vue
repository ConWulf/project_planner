<template>
  <form @submit.prevent="handleSubmit">
    <label>TITLE</label>
    <input v-model="title" type="text" requred>
    <label>DETAILS</label>
    <textarea v-model="details" required ></textarea>
    <button>ADD PROJECT</button>
  </form>
</template>

<script>
export default {
  name: "AddProject",
  data () {
    return {
      title: '',
      details: ''
    }
  },
  methods: {
    handleSubmit () {
      let project = {
        title: this.title,
        details: this.details,
        complete: false
      }
      fetch(" http://localhost:3000/projects", {
        method: "POST",
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(project)
      }).then(() => {
        this.$router.push({name: 'Home'})
      });
    }
  }
}
</script>
