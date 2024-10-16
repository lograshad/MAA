<template>
  <q-item
    clickable
    :to="link"
    :class="{
      'bg-[#09C269] rounded-xl mb-3': currRoute === link,
      'text-primary hover:bg-[#09C269] rounded-xl mb-3': true,
    }"
  >
    <q-item-section v-if="icon" avatar>
      <icon />
    </q-item-section>

    <q-item-section>
      <q-item-label class="text-white text-weight-medium">{{
        title
      }}</q-item-label>
    </q-item-section>
  </q-item>
</template>

<style>
@import 'tailwindcss/base';
@import 'tailwindcss/components';
@import 'tailwindcss/utilities';
</style>

<script setup lang="ts">
import { Component } from 'vue';
import { useRoute } from 'vue-router';

defineOptions({
  name: 'EssentialLink',
});

export interface EssentialLinkProps {
  title: string;
  caption?: string;
  link?: string;
  icon?: Component;
}
const route = useRoute();
const currRoute = route.path;

withDefaults(defineProps<EssentialLinkProps>(), {
  caption: '',
  link: '#',
});
</script>
