<template>
    <tr>
        <td class="border-right-0" width="10%">{{index+1}}</td>
        <td class="border-right-0" width="45%">{{project.name}}</td>
        <td class="border-right-0" width="35%"></td>
        <td class="border-right-0" width="10%">
            <button class="btn btn-primary btn-sm py-0 mr-1" @click.prevent="editProject(project)">
                <i class="fa fa-edit"></i>
            </button>
            <button class="btn btn-danger btn-sm py-0" @click="deleteProject(project)">
                <i class="fa fa-trash-o "></i>
            </button>

        </td>
    </tr>
</template>

<script>
  import axios from "axios";

  const $ = window.jQuery;

  export default {
    name: "TableRow",
    props: {
      index: {
        type: Number,
      },
      project: {
        type: Object,
        required: true
      }
    },
    methods: {
      editProject(project) {
        console.log(project);
      },
      deleteProject(project) {
        const self = this;
        $.simpleDialog({
          title: "Are you sure do you want to delete?",
          message: "This is not an irreversible process. Do you want to delete this project?",
          closeBtnText: "No! Cancel",
          confirmBtnText: "Yes! Delete",
          onSuccess: function () {
            axios.post("http://aptu.test/api/delete-project", {projectId: project.id})
              .then(response => {
                const responseData = response.data;
                if (responseData.success) {
                  self.$emit("on-delete", project.id);
                } else {
                  console.log(responseData.message);
                }
              });
          }
        })

      }
    }
  }
</script>

<style scoped>

</style>