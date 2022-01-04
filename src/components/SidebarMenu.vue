<template>
    <nav id="sidebarMenu" class="col-md-3 col-lg-2 d-md-block bg-light sidebar collapse">
        <div class="position-sticky pt-3">
            <ul class="nav flex-column">
                <li class="nav-item">
                    <a class="nav-link active" aria-current="page" href="/manage-projects">
                        <span data-feather="home"></span>
                        Manage Projects
                    </a>
                </li>
                <li class="nav-item">
                    <a class="nav-link active" aria-current="page" href="/time-tracker">
                        <span data-feather="home"></span>
                        Time Tracker
                    </a>
                </li>
            </ul>
        </div>
    </nav>
</template>

<script>
  export default {
    name: "SidebarMenu"
  }
</script>

<style scoped>

</style>