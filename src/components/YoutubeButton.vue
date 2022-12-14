<template>
  <div>
    <a :href="href" target="_blank"
      class="px-3 py-2 rounded border border-orange-600 hover:bg-orange-600 bg-orange-500 text-white transition-colors ">
      <slot></slot>
    </a>
  </div>
</template>

<script setup>
const props = defineProps({
  href: String
})
</script>