<script setup lang="ts">
import FlowCard from 'components/cards/FlowCard.vue';
import { supabase } from 'src/supabase';
import { onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';
import { useToast } from 'vue-toastification';
interface Flow {
  id: string;
  title: string;
  desc: string;
}
const cardList = ref<Flow[]>([]);
const isLoading = ref(false);
const typeName = ref('');
const toast = useToast();
const route = useRoute();
const typeId = route.params.id;

const fetchFlows = async () => {
  try {
    isLoading.value = true;
    const toastId = toast.info('Fetching flows...', {
      id: 'fetching-flow-toast',
    });

    const res = await supabase.from('flows').select('*').eq('type', typeId);
    if (res.error) throw res.error.details || 'Error fetching flows';

    cardList.value = res.data || [];

    const typeRes = await supabase
      .from('types')
      .select('title, description')
      .eq('id', typeId)
      .single();

    if (typeRes.error) throw typeRes.error.details || 'Error fetching type';
    typeName.value = typeRes.data.title;

    toast.dismiss(toastId);
  } catch (error) {
    toast.dismiss('fetching-flow-toast');
    toast.error(error);
  } finally {
    isLoading.value = false;
  }
};
onMounted(() => {
  fetchFlows();
});
</script>

<template>
  <div class="px-6">
    <h2 class="text-[#201D1D] text-xl font-semibold">
      Start with the essentials
    </h2>
    <p class="text-sm mt-2 mb-5 text-[#848484]">
      Start with these flows to increase revenue and engagement with little
      effort.
    </p>
    <div class="grid sm:grid-cols-2 md:grid-cols-3 gap-7">
      <FlowCard
        v-for="card in cardList"
        :key="card.title"
        v-bind="card"
        :typeName="typeName"
      />
    </div>
    <div v-if="cardList.length === 0">Add Flow to continue</div>
  </div>
</template>
