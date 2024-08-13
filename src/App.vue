<template>
  <div class="flex h-full">
    <!-- Static sidebar for desktop -->
    <Menu />

    <div class="flex min-w-0 flex-1 flex-col overflow-hidden">
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
  </div>
</template>

<script setup>
import Menu from "./components/menu.vue";
import CompanyDirectory from "./components/companyDirectory.vue";
import CompanyDetail from "./components/companyDetail.vue";

import { ref } from "vue";

const sidebarOpen = ref(false);
</script>
