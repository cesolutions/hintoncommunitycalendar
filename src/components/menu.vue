<template>
  <div class="hidden lg:flex lg:flex-shrink-0">
    <div class="flex w-64 flex-col">
      <!-- Sidebar component, swap this element with another sidebar if you like -->
      <div
        class="flex min-h-0 flex-1 flex-col border-r border-gray-200 bg-gray-100"
      >
        <div class="flex flex-1 flex-col overflow-y-auto pb-4 pt-5">
          <div class="flex flex-shrink-0 items-center px-4">
            <img
              class="h-8 w-auto"
              src="https://tailwindui.com/img/logos/mark.svg?color=pink&shade=500"
              alt="Your Company"
            />
          </div>
          <nav class="mt-5 flex-1" aria-label="Sidebar">
            <div class="space-y-1 px-2">
              <a
                v-for="item in navigation"
                :key="item.name"
                @click="menuClick(item.name)"
                :class="[
                  item.current
                    ? 'bg-gray-200 text-gray-900'
                    : 'text-gray-600 hover:bg-gray-50 hover:text-gray-900',
                  'group flex items-center rounded-md px-2 py-2 text-sm font-medium',
                ]"
                :aria-current="item.current ? 'page' : undefined"
              >
                <component
                  :is="item.icon"
                  :class="[
                    item.current
                      ? 'text-gray-500'
                      : 'text-gray-400 group-hover:text-gray-500',
                    'mr-3 h-6 w-6 flex-shrink-0',
                  ]"
                  aria-hidden="true"
                />
                {{ item.name }}
              </a>
            </div>
            <hr class="my-5 border-t border-gray-200" aria-hidden="true" />
            <div class="flex-1 space-y-1 px-2">
              <a
                v-for="item in secondaryNavigation"
                :key="item.name"
                @click="menuClick(item.name)"
                class="group flex items-center rounded-md px-2 py-2 text-sm font-medium text-gray-600 hover:bg-gray-50 hover:text-gray-900"
              >
                <component
                  :is="item.icon"
                  class="mr-3 h-6 w-6 flex-shrink-0 text-gray-400 group-hover:text-gray-500"
                  aria-hidden="true"
                />
                {{ item.name }}
              </a>
            </div>
          </nav>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";
import {
  Dialog,
  DialogPanel,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import {
  Bars3Icon,
  CalendarIcon,
  CogIcon,
  HomeIcon,
  LifebuoyIcon,
  MagnifyingGlassCircleIcon,
  MapIcon,
  MegaphoneIcon,
  SquaresPlusIcon,
  UserGroupIcon,
  XMarkIcon,
  ShareIcon,
} from "@heroicons/vue/24/outline";
import {
  ChevronLeftIcon,
  EnvelopeIcon,
  FunnelIcon,
  MagnifyingGlassIcon,
  PhoneIcon,
} from "@heroicons/vue/20/solid";

const emit = defineEmits(["menuChange"]);

const navigation = [
  { name: "Home", href: "#", icon: HomeIcon, current: false },
  {
    name: "Directory",
    href: "#",
    icon: MagnifyingGlassCircleIcon,
    current: true,
  },
  { name: "Map", href: "#", icon: MapIcon, current: false },
];
const secondaryNavigation = [
  { name: "Want to help?", href: "#", icon: LifebuoyIcon },
];
const state = reactive({
  page: "",
});

function menuClick(pageName) {
  //emit the menu selection to the parent component, so the page can be changed.
  state.page = pageName;
  console.log(`Child: ${state.page}`);
  emit("menuChange", state.page);
}
</script>
