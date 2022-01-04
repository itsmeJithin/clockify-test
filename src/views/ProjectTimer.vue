<template>
    <div class="full-width">
        <div class="col-12">
            <h4>Available Projects</h4>
        </div>
        <div class="col-12">
            <ListAllProjectsTimerTable :projects="projects"/>
        </div>
    </div>
</template>

<script>
  import ListAllProjectsTimerTable from '../components/timeTracker/ListAllProjectTimerTable';
  import axios from 'axios';

  export default {
    name: "ProjectTimer",
    components: {ListAllProjectsTimerTable},
    data() {
      return {
        projects: []
      }
    },
    mounted() {
      this.getAllProjects();
    },
    methods: {
      getAllProjects() {
        axios.get("http://aptu.test/api/get-all-projects-with-timer")
          .then(response => {
            const responseData = response.data;
            if (responseData.success) {
              this.projects = responseData.data;
            } else {
              console.log(responseData.message);
            }
          })
          .catch(error => {
            console.log(error);
          })
      }
    }
  }
</script>

<style scoped>

</style>