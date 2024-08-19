<template>
  <div id="vueapp" class="flex h-full">
    <!-- Static sidebar for desktop -->
    <Menu @menuChange="onMenuChange" />

    <div v-if="state.activePage == 'Home'">
      <Home />
    </div>

    <!--This is the company directory pages.-->
    <div
      v-show="state.activePage == 'Directory'"
      class="flex min-w-0 flex-1 flex-col overflow-hidden"
    >
      <div class="relative z-0 flex flex-1 overflow-hidden">
        <main
          class="relative z-0 flex-1 overflow-y-auto focus:outline-none xl:order-last"
        >
          <CompanyDetail />
        </main>
        <aside
          class="hidden w-96 flex-shrink-0 border-r border-gray-200 xl:order-first xl:flex xl:flex-col"
        >
          <CompanyDirectory />
        </aside>
      </div>
    </div>

    <div v-show="state.activePage == 'Map'">
      <h1>Map page</h1>
    </div>

    <div v-show="state.activePage == 'Want to help?'">
      <h1>Help page</h1>
    </div>
  </div>
</template>

<script setup>
import Menu from "./components/menu.vue";
import CompanyDirectory from "./components/companyDirectory.vue";
import CompanyDetail from "./components/companyDetail.vue";
import Home from "./components/home.vue";
import { defineComponent, reactive } from "vue";

const state = reactive({
  activePage: "Directory",
});

function onMenuChange(selectedPage) {
  console.log(`Parent: ${selectedPage}`);
  state.activePage = selectedPage;
}
</script>
