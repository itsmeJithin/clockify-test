<template>
    <div class="modal fade" :class="showModal?'show':''" id="staticBackdrop" data-bs-backdrop="static"
         data-bs-keyboard="false" tabindex="-1"
         aria-labelledby="staticBackdropLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="staticBackdropLabel">Create Project</h5>
                    <i class="fa fa-times" @click.prevent="onClose" aria-label="Close"/>
                </div>
                <div class="modal-body">
                    <form action="">
                        <div class="row">
                            <div class="col-12 form-group">
                                <label for="project-name">Project Name</label>
                                <input class="form-control" type="text" id="project-name" name="project-name"
                                       v-model="projectName" placeholder="Enter your project name">
                            </div>
                            <div class="col-12 form-group">
                                <label for="project-description">Project Description</label>
                                <input class="form-control" type="text" id="project-description"
                                       name="project-description"
                                       placeholder="Enter your project description"
                                       v-model="projectDescription">
                            </div>
                        </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" @click.prevent="onClose">Close</button>
                    <button type="button" class="btn btn-primary" @click.prevent="saveProject">Save</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
  import axios from "axios";

  export default {
    name: "CreateProjectSliderModal",
    props: {
      showModal: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {
        projectName: "",
        projectDescription: ""
      }
    },
    methods: {
      saveProject() {
        const formData = {
          name: this.projectName,
          description: this.projectDescription
        };
        axios.post("http://aptu.test/api/create-or-update-project", formData)
          .then(response => {
            console.log(response.data);
            this.reset();
          })
          .catch(error => {
            console.log(error);
          });
      },
      reset() {
        this.projectName = "";
        this.projectDescription = "";
      },
      onClose() {
        this.reset();
        this.$emit("on-close-slider");
      }
    }
  }
</script>

<style scoped>

</style>