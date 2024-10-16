<script setup lang="ts">
defineOptions({
  name: 'FlowCard',
});

export interface FlowCardProps {
  id: string;
  title: string;
  desc: string;
}

defineProps({
  id: String,
  title: String,
  desc: String,
  typeName: String,
});

import { ref } from 'vue';
const showFlowDetails = ref(false);
</script>

<template>
  <div
    @click="showFlowDetails = true"
    class="relative rounded-xl shadow-lg h-full flex flex-col cursor-pointer"
  >
    <div class="p-5 flex-grow flex flex-col">
      <h4 class="text-[16px] text-[#201D1D] my-2 font-medium">{{ title }}</h4>
      <div class="flex items-center gap-3 py-3">
        <p class="text-[#201D1D] text-[16px] font-medium">{{ typeName }}</p>
        <q-icon name="arrow_forward" size="xs" color="grey-7" />
      </div>
      <p class="text-[#848484] text-sm pb-2">
        {{ desc }}
      </p>
      <div class="mt-auto flex items-center justify-between">
        <div
          class="bg-[#E6F9F0] text-sm cursor-pointer flex font-medium w-fit text-[#09C269] py-1 px-3 rounded-2xl"
        >
          Shopify
        </div>
        <q-icon name="mail" size="xs" color="grey-7" />
      </div>
    </div>
  </div>
  <q-dialog v-model="showFlowDetails">
    <q-card style="width: 1200px; border-radius: 20px; max-width: 80vw">
      <div class="bg-white rounded-xl p-10">
        <div
          class="justify-between flex items-center pb-2 border-b border-[#DDDEE2]"
        >
          <span class="text-[22px] text-[#201D1D] font-medium">{{
            title
          }}</span>
          <q-icon
            name="close"
            @click="showFlowDetails = false"
            size="sm"
            class="cursor-pointer"
          />
        </div>
        <div class="flex items-start">
          <div class="border-r px-5 w-[45%] pt-5 border-[#DDDEE2]">
            <div class="border-[#DDDEE2] pb-5 border-b">
              <div class="text-[16px] font-medium">Description</div>
              <p class="text-[#848484] text-sm">{{ desc }}</p>
            </div>
            <div class="border-[#DDDEE2] pb-5 border-b">
              <div class="text-[16px] font-medium mt-2">Name</div>
              <p
                class="text-[#848484] text-sm p-5 border rounded-md border-[#DDDEE2]"
              >
                {{ title }} - {{ typeName }}
              </p>
            </div>
            <div class="border-[#DDDEE2] pb-5 border-b">
              <div class="text-[16px] font-medium mt-2">Tags</div>
              <select
                id="tags"
                class="w-full border rounded-md text-sm pt-4 mt-1 px-2 pb-2 mb-2 border-[#DDDEE2] outline-none"
              >
                <option value="1">Tag One</option>
                <option value="2">Tag Two</option>
                <option value="1">Tag Three</option>
              </select>
            </div>
          </div>
          <div></div>
        </div>
      </div>
    </q-card>
  </q-dialog>
</template>
