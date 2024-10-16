<script setup lang="ts">
import CloseIcon from '../icons/CloseIcon.vue';
import IncrementIcon from '../icons/IncrementIcon.vue';

defineOptions({
  name: 'MainCard',
});

export interface MainCardProps {
  id: number;
  title: string;
  description: string;
  hint: string;
}

withDefaults(defineProps<MainCardProps>(), {
  // img: 'https://via.placeholder.com/150',
});
</script>

<template>
  <div class="relative rounded-xl shadow-lg h-full flex flex-col">
    <div>
      <!-- <img :src="img" alt="" width="50" /> -->
    </div>
    <CloseIcon class="absolute top-2 right-2 cursor-pointer" />
    <div class="p-5 flex-grow flex flex-col">
      <h4 class="text-[16px] text-[#201D1D] my-2 font-medium">{{ title }}</h4>
      <p class="text-[#848484] text-sm pb-2 border-b border-[#DDDEE2]">
        {{ description }}
      </p>
      <div class="flex items-start gap-3 py-3">
        <IncrementIcon />
        <p class="text-[#201D1D] text-sm">{{ hint }}</p>
      </div>
      <div
        @click="() => $router.push({ path: `/flows/${id}` })"
        class="bg-[#E6F9F0] text-sm mt-auto cursor-pointer flex font-medium w-fit text-[#09C269] p-3 rounded-lg"
      >
        Get Started
      </div>
    </div>
  </div>
</template>
