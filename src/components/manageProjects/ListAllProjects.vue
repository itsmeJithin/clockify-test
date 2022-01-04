<template>
    <table class="table table-striped">
        <tbody v-if="projects.length">
        <table-row v-for="(project,index) in projects" :key="project.id" :project="project" :index="index">
        </table-row>
        </tbody>
        <tbody v-else>
        <tr>
            <td colspan="4" class="text-center text-muted">
                No projects available
            </td>
        </tr>
        </tbody>
    </table>
</template>

<script>
  import TableRow from './TableRow';

  export default {
    name: "ListAllProjects",
    components: {TableRow},
    props: {
      projects: {
        type: Array,
        default() {
          return [];
        }
      }
    }
  }
</script>

<style scoped>

</style>