<script setup>
import NavItem from "@/components/NavItem.vue";
import {HomeIcon, NewspaperIcon, PhotographIcon} from "@heroicons/vue/24/outline";

const navItems = [
  {href: "#", open: false, label: "Dashboard", children: [], icon: HomeIcon},
  {
    href: "#", open: false,
    label: "Posts",
    children: [
      {href: "#", open: false, label: "All posts", children: [], icon: null},
      {href: "#", open: false, label: "Add new", children: [], icon: null},
      {href: "#", open: false, label: "Categories", children: [], icon: null},
    ],
    icon: NewspaperIcon,
  },
  {
    href: "#", open: false,
    label: "Media",
    children: [
      {href: "#", open: false, label: "Library", children: [], icon: null},
      {
        href: "#", open: false,
        label: "Add new",
        children: [{href: "#", open: false, label: "Third level", children: [], icon: null}],
        icon: null,
      },
    ],
    icon: PhotographIcon,
  },
];
</script>
<template>
  <div class="flex min-h-screen">
    <nav class="w-64 shrink-0 shadow-md bg-indigo-600 py-4">
      <div class="px-4">
        <a
          href="#"
          class="inline-block w-full"
        >
          <img class="h-8 w-auto mx-auto" src="https://tailwindui.com/img/logos/mark.svg?color=white" alt="Your Company" />
        </a>
      </div>

      <div class="mt-6 px-2">
        <NavItem
          :item="item"
          v-for="item in navItems"
          :key="item.label"
        />
      </div>
    </nav>

    <main class="flex-1">
      <div class="py-6">
        <div class="mx-auto max-w-7xl px-4 sm:px-6 md:px-8">
          <h1 class="text-2xl font-semibold text-gray-900">Dashboard</h1>
        </div>
        <div class="mx-auto max-w-7xl px-4 sm:px-6 md:px-8">
          <div class="py-4">
            <div class="h-96 rounded-lg border-4 border-dashed border-gray-200" />
          </div>
        </div>
      </div>
    </main>
  </div>
</template>