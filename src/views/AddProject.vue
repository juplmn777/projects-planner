<template>
  <form @submit.prevent="handleSubmit">
    <label>Project title:</label>
    <input type="text" v-model="title" required />
    <label>Project details</label>
    <textarea v-model="details" required></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: null,
      details: null,
    };
  },
  methods: {
    handleSubmit() {
      let project = {
        title: this.title,
        details: this.details,
        complete: false,
      };

      fetch('http://localhost:3000/projects', {
        method: 'POST',
        headers: { 'Content-type': 'application/json' },
        body: JSON.stringify(project),
      })
        .then(() => {
          this.$router.push('/');
        })
        .catch((error) => console.log(error));
    },
  },
};
</script>

<style scoped>
form {
  background: #fff;
  padding: 20px;
  border-radius: 10px;
}

label {
  display: block;
  color: #30475e;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}

input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
  height: 50px;
  outline: none;
}

textarea {
  border: 1px solid #ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
  outline: none;
}

form button {
  display: block;
  margin: 20px auto 0;
  background: #3fa796;
  color: #fff;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>
