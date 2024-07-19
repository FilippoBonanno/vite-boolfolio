<script>
import axios from 'axios';
import SingleCard from './components/SingleCard.vue';



export default {
  name: 'App',

  components: {
    SingleCard,
  },

  data() {
    return {
      base_url: 'http://localhost:8000',
      projects: '',
      isActive: false
    }
  },

  methods: {
    nextPage() {
      axios.get('http://localhost:8000/api/projects?page=2').then(response => {
        this.projects = response.data.projects.data;
      })
    },

    prevPage() {
      axios.get('http://localhost:8000/api/projects?page=1').then(response => {
        this.projects = response.data.projects.data;
      })
    },

    clickPage(element) {
      axios.get(element).then(response => {
        this.projects = response.data.projects;
        console.log(this.projects.links)
      })
    }
  },

  mounted() {
    axios.get('http://localhost:8000/api/projects').then(response => {
      console.log(response);
      this.projects = response.data.projects;

      console.log(this.projects)

    })
  }
}

</script>

<template>
  <h1>ciao</h1>
  <div class="container">
    <nav aria-label="...">
      <ul class="pagination">
        <template v-for="link in projects.links">
          <li class="page-item" :class="{ active: link.active }">
            <a class="page-link" @click="clickPage(link.url)" href="#">{{ link.label }}</a>
          </li>

        </template>

      </ul>
    </nav>

    <div class="row">
      <div class="col-12 d-flex flex-wrap justify-content-center">
        <template v-for="project in projects.data">
          <SingleCard :card="project" />
        </template>
      </div>
    </div>
  </div>

</template>

<style scoped></style>