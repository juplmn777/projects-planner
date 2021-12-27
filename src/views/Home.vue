<template>
  <div class="home">
    <TheFilterNav
      @filterChange="currentFilter = $event"
      :currentFilter="currentFilter"
    />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @delete="handleDeleteProject"
          @complete="handleCompleteProject"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '@/components/SingleProject.vue';
import TheFilterNav from '@/components/TheFilterNav.vue';
export default {
  name: 'Home',
  components: {
    SingleProject,
    TheFilterNav,
  },
  data() {
    return {
      projects: [],
      currentFilter: 'all',
    };
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then((response) => response.json())
      .then((data) => (this.projects = data))
      .catch((error) => console.log(error.message));
  },
  methods: {
    handleDeleteProject(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
    },
    handleCompleteProject(id) {
      let p = this.projects.find((project) => {
        return project.id === id;
      });
      p.complete = !p.complete;
    },
  },
  computed: {
    filteredProjects() {
      if (this.currentFilter === 'completed') {
        return this.projects.filter((project) => project.complete);
      }
      if (this.currentFilter === 'inprogress') {
        return this.projects.filter((project) => !project.complete);
      }
      return this.projects;
    },
  },
};
</script>

<style scoped>
.home {
  font-size: 1.2rem;
}
</style>
