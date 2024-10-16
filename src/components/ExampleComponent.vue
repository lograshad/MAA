<template>
  <div class="px-6">
    <h2 class="text-[#201D1D] text-xl font-semibold">
      Maximize Revenue with Flows
    </h2>
    <p class="text-sm mt-2 mb-5 text-[#848484]">
      Drive up revenue and engagement with key automations that are pre-built
      and ready to turn on!
    </p>
    <div class="grid sm:grid-cols-2 md:grid-cols-3 gap-7">
      <MainCard v-for="card in cardList" :key="card.title" v-bind="card" />
    </div>
    <div v-if="cardList.length === 0">Add Flow Types to continue</div>
  </div>
</template>

<script setup lang="ts">
import MainCard from 'components/cards/MainCard.vue';
import { supabase } from 'src/supabase';
import { onMounted, ref } from 'vue';
import { useToast } from 'vue-toastification';

interface Type {
  id: number;
  title: string;
  description: string;
  hint: string;
}

const cardList = ref<Type[]>([]);
const isLoading = ref(false);
const toast = useToast();

const fetchTypes = async () => {
  try {
    isLoading.value = true;
    const toastId = toast.info('Fetching types...', {
      id: 'fetching-type-toast',
    });

    const res = await supabase.from('types').select('*');

    if (res.error) throw res.error.details || 'Error fetching types';

    cardList.value = res.data || [];

    toast.dismiss(toastId);
  } catch (error) {
    toast.dismiss('fetching-type-toast');
    toast.error(error);
  } finally {
    isLoading.value = false;
  }
};

onMounted(() => {
  fetchTypes();
});
</script>
