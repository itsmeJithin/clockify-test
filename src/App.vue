<template>
    <div id="app">
        <div class="row full-height-vh">
            <sidebar-menu/>
            <main class="col-md-9 ms-sm-auto col-lg-10 px-md-4">
                <div class="d-flex justify-content-between flex-wrap flex-md-nowrap align-items-center pt-3 pb-2 mb-3 border-bottom">
                    <h1 class="h2">Clockify Demo</h1>
                </div>
              <div class="row">
                <router-view/>
              </div>
            </main>
        </div>

    </div>
</template>

<style>
</style>
<script>
  import SidebarMenu from './components/SidebarMenu';

  export default {
    components: {SidebarMenu}
  }
</script>