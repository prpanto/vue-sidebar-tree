<script setup>
import {computed} from "vue";
import {Disclosure, DisclosureButton, DisclosurePanel} from "@headlessui/vue";
import {ChevronDownIcon} from "@heroicons/vue/24/solid";
import {v4 as uuid} from "uuid";

const props = defineProps({
  item: Object,
});

const hasOpenChild = computed(() => {
  function hasOpenItem(items) {
    return items.some(item => item.open || hasOpenItem(item.children));
  }

  return hasOpenItem(props.item.children);
});
</script>
<template>
  <a
    v-if="!item.children.length"
    :class="[
      'group flex w-full items-center rounded-md py-2 px-3 text-sm',
      'hover:bg-gray-100',
      item.open ? 'font-semibold text-gray-900' : 'font-medium text-gray-100 hover:text-gray-900',
    ]"
    :href="item.href"
    :key="`sidebar-${uuid}`"
  >
    <component
      :class="[
        'mr-2 h-6 w-6 shrink-0 group-hover:text-gray-600',
        item.open ? 'text-gray-900' : 'text-gray-100',
      ]"
      :is="item.icon"
      v-if="item.icon"
    ></component>
    <span>{{ item.label }}</span>
  </a>

  <Disclosure
    v-else
    v-slot="{open}"
    :default-open="hasOpenChild"
  >
    <DisclosureButton
      as="a"
      :class="[
        'group flex w-full items-center rounded-md py-2 px-3 text-left text-sm',
        'hover:bg-gray-100',
        open ? 'font-semibold text-gray-100 hover:text-gray-900' : 'font-medium text-gray-100 hover:text-gray-900',
      ]"
      :key="`sidebar-${uuid}`"
    >
      <component
        :class="[
          'mr-2 h-6 w-6 shrink-0 group-hover:text-gray-600',
          open ? 'text-gray-100' : 'text-gray-100 hover:text-gray-900',
        ]"
        :is="item.icon"
        v-if="item.icon"
      ></component>
      
      <span class="flex-1">{{ item.label }}</span>

      <ChevronDownIcon
        :class="[
          'h-6 w-6 shrink-0',
          open ? '-rotate-180 text-gray-100 group-hover:text-gray-900' : 'text-gray-100 group-hover:text-gray-900',
        ]"
      />
    </DisclosureButton>

    <transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="transform scale-95 opacity-0"
      enter-to-class="transform scale-100 opacity-100"
      leave-active-class="transition duration-300 ease-out"
      leave-from-class="transform scale-100 opacity-100"
      leave-to-class="transform scale-95 opacity-0"
    >
      <DisclosurePanel class="ml-4">
        <NavItem
          v-for="child in item.children"
          :key="`sidebar-${uuid()}`"
          :item="child"
        />
      </DisclosurePanel>
    </transition>
  </Disclosure>
</template>