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
      console.log(this.title, this.details);
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
  color: #bbb;
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
  height: 100px;
}

textarea {
  border: 1px solid #ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
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
