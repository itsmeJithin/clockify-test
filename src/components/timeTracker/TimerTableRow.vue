<template>
    <tr>
        <td class="border-right-0" width="10%">{{index+1}}</td>
        <td class="border-right-0" width="45%">{{project.name}}</td>
        <td class="border-right-0" width="35%">
            {{time|formatTime}}
        </td>
        <td class="border-right-0" width="10%">
            <button class="btn btn-danger btn-sm py-0 mr-1" v-if="project.time" @click.prevent="stopTimer(project)">
                <i class="fa fa-stop"></i>
            </button>
            <button class="btn btn-success btn-sm py-0" v-else @click="startTimer(project)">
                <i class="fa fa-play "></i>
            </button>

        </td>
    </tr>
</template>

<script>
  import axios from "axios";
  import moment from "moment";

  const $ = window.jQuery;

  export default {
    name: "TimerTableRow",
    props: {
      index: {
        type: Number,
      },
      project: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
        time: this.project.time?this.project.time:0
      }
    },
    filters: {
      formatTime(value) {
        let duration = moment.duration(value, "seconds");
        return duration.hours() + ":" + duration.minutes() + ":" + duration.seconds()
      }
    },
    methods: {
      startTimer(project) {
        axios.post("http://aptu.test/api/start-time", {projectId: project.id})
          .then(response => {
            const responseData = response.data;
            if (responseData.success) {
              self.$emit("on-delete", project.id);
            } else {
              console.log(responseData.message);
            }
          });
      },
      stopTimer(project) {
        const self = this;
        $.simpleDialog({
          title: "Are you sure?",
          message: "Do you want to stop the timer for this project?",
          closeBtnText: "No! Cancel",
          confirmBtnText: "Yes! Stop",
          onSuccess: function () {
            axios.post("http://aptu.test/api/stop-timer", {projectId: project.id})
              .then(response => {
                const responseData = response.data;
                if (responseData.success) {
                  self.$emit("on-delete", project.id);
                } else {
                  console.log(responseData.message);
                }
              });
          }
        });
      }
    }
  }
</script>

<style scoped>

</style>