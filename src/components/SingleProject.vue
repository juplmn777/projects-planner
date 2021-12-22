<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="toggleDetails">{{ project.title }}</h3>
      <div class="icons">
        <span class="material-icons"> edit </span>
        <span class="material-icons" @click="deleteProject"> delete </span>
        <span class="material-icons tick" @click="toggleCompleteProject">
          done
        </span>
      </div>
    </div>
    <div class="details" v-if="showDetails">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['project'],
  data() {
    return {
      showDetails: false,
      uri: 'http://localhost:3000/projects/' + this.project.id,
    };
  },
  methods: {
    toggleDetails() {
      this.showDetails = !this.showDetails;
    },
    deleteProject() {
      fetch(this.uri, { method: 'DELETE' }).then(() => {
        this.$emit('delete', this.project.id).catch((error) =>
          console.log(error.message)
        );
      });
    },
    toggleCompleteProject() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-type': 'application/json' },
        body: JSON.stringify({ complete: !this.project.complete }),
      })
        .then(() => {
          this.$emit('complete', this.project.id);
        })
        .catch((error) => console.log(error));
    },
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  padding: 10px 20px;
  border-radius: 5px;
  background: #fff;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.1);
  border-left: 4px solid #f05454;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.material-icons {
  margin-left: 10px;
  transition: 0.3s;
  cursor: pointer;
}

.material-icons:hover {
  color: #dddddd;
  transform: scale(1.2);
}

.project.complete {
  border-left: 4px solid #3fa796;
}

.project.complete .tick {
  color: #3fa796;
}
</style>
