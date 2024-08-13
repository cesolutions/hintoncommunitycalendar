<template>
  <!-- Breadcrumb -->
  <nav
    class="flex items-start px-4 py-3 sm:px-6 lg:px-8 xl:hidden"
    aria-label="Breadcrumb"
  >
    <a
      href="#"
      class="inline-flex items-center space-x-3 text-sm font-medium text-gray-900"
    >
      <ChevronLeftIcon class="-ml-2 h-5 w-5 text-gray-400" aria-hidden="true" />
      <span>Directory</span>
    </a>
  </nav>

  <article>
    <!-- Profile header -->
    <div>
      <div>
        <img
          class="h-32 w-full object-cover lg:h-48"
          :src="profile.coverImageUrl"
          alt=""
        />
      </div>
      <div class="mx-auto max-w-5xl px-4 sm:px-6 lg:px-8">
        <div class="-mt-12 sm:-mt-16 sm:flex sm:items-end sm:space-x-5">
          <div class="flex">
            <img
              class="h-24 w-24 rounded-full ring-4 ring-white sm:h-32 sm:w-32"
              :src="profile.imageUrl"
              alt=""
            />
          </div>
          <div
            class="mt-6 sm:flex sm:min-w-0 sm:flex-1 sm:items-center sm:justify-end sm:space-x-6 sm:pb-1"
          >
            <div class="mt-6 min-w-0 flex-1 sm:hidden 2xl:block">
              <h1 class="truncate text-2xl font-bold text-gray-900">
                {{ profile.name }}
              </h1>
            </div>
            <div
              class="mt-6 flex flex-col justify-stretch space-y-3 sm:flex-row sm:space-x-4 sm:space-y-0"
            >
              <button
                type="button"
                class="inline-flex justify-center gap-x-1.5 rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
              >
                <MapIcon
                  class="-ml-0.5 h-5 w-5 text-gray-500"
                  aria-hidden="true"
                />
                Show on map
              </button>
              <button
                type="button"
                class="inline-flex justify-center gap-x-1.5 rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
              >
                <ShareIcon
                  class="-ml-0.5 h-5 w-5 text-gray-500"
                  aria-hidden="true"
                />
                Share
              </button>
            </div>
          </div>
        </div>
        <div class="mt-6 hidden min-w-0 flex-1 sm:block 2xl:hidden">
          <h1 class="truncate text-2xl font-bold text-gray-900">
            {{ profile.name }}
          </h1>
        </div>
      </div>
    </div>

    <!-- Tabs -->
    <div class="mt-6 sm:mt-2 2xl:mt-5">
      <div class="border-b border-gray-200">
        <div class="mx-auto max-w-5xl px-4 sm:px-6 lg:px-8">
          <nav class="-mb-px flex space-x-8" aria-label="Tabs">
            <a
              v-for="tab in tabs"
              :key="tab.name"
              :href="tab.href"
              :class="[
                tab.current
                  ? 'border-pink-500 text-gray-900'
                  : 'border-transparent text-gray-500 hover:border-gray-300 hover:text-gray-700',
                'whitespace-nowrap border-b-2 px-1 py-4 text-sm font-medium',
              ]"
              :aria-current="tab.current ? 'page' : undefined"
              >{{ tab.name }}</a
            >
          </nav>
        </div>
      </div>
    </div>

    <!-- Description list -->
    <div class="mx-auto mt-6 max-w-5xl px-4 sm:px-6 lg:px-8">
      <dl class="grid grid-cols-2 gap-x-4 gap-y-8 sm:grid-cols-2">
        <div
          v-for="field in Object.keys(profile.fields)"
          :key="field"
          class="sm:col-span-1"
        >
          <dt class="text-sm font-medium text-gray-500">{{ field }}</dt>
          <dd class="mt-1 text-sm text-gray-900">
            {{ profile.fields[field] }}
          </dd>
        </div>
        <div class="sm:col-span-2">
          <dt class="text-sm font-medium text-gray-500">About</dt>
          <dd
            class="mt-1 max-w-prose space-y-5 text-sm text-gray-900"
            v-html="profile.about"
          />
        </div>
      </dl>
    </div>

    <!-- Team member list -->
    <div class="mx-auto mt-8 max-w-5xl px-4 pb-12 sm:px-6 lg:px-8">
      <h2 class="text-sm font-medium text-gray-500">Related businesses?</h2>
      <div class="mt-1 grid grid-cols-1 gap-4 sm:grid-cols-2">
        <div
          v-for="person in team"
          :key="person.handle"
          class="relative flex items-center space-x-3 rounded-lg border border-gray-300 bg-white px-6 py-5 shadow-sm focus-within:ring-2 focus-within:ring-pink-500 focus-within:ring-offset-2 hover:border-gray-400"
        >
          <div class="flex-shrink-0">
            <img class="h-10 w-10 rounded-full" :src="person.imageUrl" alt="" />
          </div>
          <div class="min-w-0 flex-1">
            <a href="#" class="focus:outline-none">
              <span class="absolute inset-0" aria-hidden="true" />
              <p class="text-sm font-medium text-gray-900">
                {{ person.name }}
              </p>
              <p class="truncate text-sm text-gray-500">
                {{ person.role }}
              </p>
            </a>
          </div>
        </div>
      </div>
    </div>
  </article>
</template>

<script setup>
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
const tabs = [{ name: "Information", href: "#", current: true }];
//this profile detail will get populated from the db.
const profile = {
  name: "JD&C Services",
  imageUrl: "https://jdcservices.ca/img/JD&C%20Logo%20Icon%20(Transparent).png",
  coverImageUrl:
    "https://images.unsplash.com/photo-1444628838545-ac4016a5418a?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80",
  about: `
        <p>Tincidunt quam neque in cursus viverra orci, dapibus nec tristique. Nullam ut sit dolor consectetur urna, dui cras nec sed. Cursus risus congue arcu aenean posuere aliquam.</p>
        <p>Et vivamus lorem pulvinar nascetur non. Pulvinar a sed platea rhoncus ac mauris amet. Urna, sem pretium sit pretium urna, senectus vitae. Scelerisque fermentum, cursus felis dui suspendisse velit pharetra. Augue et duis cursus maecenas eget quam lectus. Accumsan vitae nascetur pharetra rhoncus praesent dictum risus suspendisse.</p>
    `,
  fields: {
    Hours: "8AM - 5PM, Monday - Friday",
    Contact: "(780) 865-6807",
    Address: "522 East River Road, Hinton, AB, T7V 2G3",
  },
};
const team = [
  {
    name: "Leslie Alexander",
    handle: "lesliealexander",
    role: "Co-Founder / CEO",
    imageUrl:
      "https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80",
  },
  {
    name: "Michael Foster",
    handle: "michaelfoster",
    role: "Co-Founder / CTO",
    imageUrl:
      "https://images.unsplash.com/photo-1519244703995-f4e0f30006d5?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80",
  },
  {
    name: "Dries Vincent",
    handle: "driesvincent",
    role: "Business Relations",
    imageUrl:
      "https://images.unsplash.com/photo-1506794778202-cad84cf45f1d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80",
  },
  {
    name: "Lindsay Walton",
    handle: "lindsaywalton",
    role: "Front-end Developer",
    imageUrl:
      "https://images.unsplash.com/photo-1517841905240-472988babdf9?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80",
  },
];
</script>
