<template>
    <div class="full-width">
        <div class="col-12 text-right">
            <button class="btn btn-primary pull-right" @click="showCreateProjectModal()">
                Create Project
            </button>
        </div>
        <div class="col-12">
            <h4>Available Projects</h4>
        </div>
        <div class="col-12 mt-3">
            <list-all-projects :projects="projects"/>
        </div>
        <CreateProjectSliderModal :show-modal="showCreateModal" @on-close-slider="onCloseSlider()"/>
    </div>
</template>

<script>
  import axios from "axios";
  import ListAllProjects from '../components/manageProjects/ListAllProjects';
  import CreateProjectSliderModal from '../components/manageProjects/CreateProjectSliderModal';

  export default {
    name: "ManageProject",
    components: {CreateProjectSliderModal, ListAllProjects},
    data() {
      return {
        projects: [],
        showCreateModal: false
      }
    },
    mounted() {
      this.getAllProjects();
    },
    methods: {
      showCreateProjectModal() {
        this.showCreateModal = true;
      },
      onCloseSlider() {
        this.showCreateModal = false;
      },
      getAllProjects() {
        axios.get("http://aptu.test/api/get-all-projects")
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