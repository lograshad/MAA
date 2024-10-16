<template>
  <div class="mb-3">
    <div
      class="border-b border-[#DDDEE2] py-4 flex items-center justify-between"
    >
      <div class="w-2/5 flex items-center ml-[5%]">
        <q-btn
          flat
          dense
          round
          icon="menu"
          color="black"
          class="lg:hidden"
          aria-label="Menu"
          @click="toggleLeftDrawer as () => void"
        />
        <div
          class="md:bg-[#F9FAFB] rounded-xl flex space-x-2 items-center md:w-[80%] p-3 ml-4 lg:ml-[10%]"
        >
          <svg
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <g clip-path="url(#clip0_515_2237)">
              <path
                d="M10.97 19.19C6.43 19.19 2.75 15.51 2.75 10.97C2.75 6.43 6.43 2.75 10.97 2.75C15.51 2.75 19.19 6.43 19.19 10.97C19.19 15.51 15.51 19.19 10.97 19.19Z"
                stroke="#848484"
                stroke-width="1.5"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
              <path
                d="M21.25 21.25L17.14 17.14"
                stroke="#848484"
                stroke-width="1.5"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </g>
            <defs>
              <clipPath id="clip0_515_2237">
                <rect width="24" height="24" fill="white" />
              </clipPath>
            </defs>
          </svg>
          <input
            placeholder="Search here.."
            class="bg-transparent outline-none border-none hidden md:w-[80%] text-[#848484]"
          />
        </div>
      </div>
      <div class="flex space-x-2 items-center mr-6">
        <q-avatar>
          <img src="https://cdn.quasar.dev/img/avatar.png" />
        </q-avatar>
        <div>
          <span class="text-sm font-medium block text-[#201D1D]"
            >Hussein Ahmed</span
          >
          <span class="text-[#848484]">Admin</span>
        </div>
      </div>
    </div>
    <div
      class="flex justify-between items-center mb-3x mx-6 py-5 border-b border-[#DDDEE2]"
    >
      <div class="text-[#201D1D] text-[22px] font-semibold">Flows</div>
      <div
        @click="createFlow = true"
        v-if="route.path.includes('/flows')"
        class="bg-[#09C269] text-sm cursor-pointer font-medium w-fit text-[#F9FAFB] p-3 rounded-lg"
      >
        Create Flow
      </div>
      <div
        @click="createType = true"
        v-else
        class="bg-[#09C269] text-sm cursor-pointer font-medium w-fit text-[#F9FAFB] p-3 rounded-lg"
      >
        Create Type
      </div>
    </div>
  </div>
  <q-dialog v-model="createFlow">
    <div class="bg-white rounded-xl p-8">
      <div
        class="justify-between flex items-center pb-2 mb-3 border-b border-[#DDDEE2]"
      >
        <span class="text-[22px] text-[#201D1D] font-medium">Create Flow</span>
        <q-icon
          name="close"
          @click="createFlow = false"
          size="sm"
          class="cursor-pointer"
        />
      </div>
      <form @submit.prevent="addFlow">
        <label class="text-[16px] font-medium" for="flowName">Flow Name</label>
        <input
          type="text"
          id="flowName"
          v-model="flowName"
          placeholder="Enter name"
          class="w-full border rounded-md text-sm pt-4 mt-1 px-2 pb-2 mb-2 border-[#DDDEE2] outline-none"
        />
        <label class="text-[16px] font-medium" for="flowDescription"
          >Flow Description</label
        >
        <textarea
          type="text"
          id="flowDescription"
          v-model="flowDescription"
          placeholder="Enter Description"
          class="w-full border rounded-md text-sm pt-4 mt-1 px-2 pb-2 mb-2 border-[#DDDEE2] outline-none"
        />
        <label class="text-[16px] font-medium" for="flowType">Flow Type</label>
        <select
          id="flowType"
          v-model="flowType"
          class="w-full border rounded-md text-sm pt-4 mt-1 px-2 pb-2 mb-2 border-[#DDDEE2] outline-none"
        >
          <option value="" disabled>Select Flow Type</option>
          <option v-for="type in cardList" :key="type.id" :value="type.id">
            {{ type.title }}
          </option>
        </select>
        <button
          type="submit"
          class="bg-[#E6F9F0] text-[#09C269] rounded-lg text-sm font-medium w-fit p-3 mt-3"
        >
          Add Type
        </button>
      </form>
    </div>
  </q-dialog>
  <q-dialog v-model="createType">
    <div class="bg-white rounded-xl p-8">
      <div
        class="justify-between flex items-center pb-2 mb-3 border-b border-[#DDDEE2]"
      >
        <span class="text-[22px] text-[#201D1D] font-medium">Create Type</span>
        <q-icon
          name="close"
          @click="createType = false"
          size="sm"
          class="cursor-pointer"
        />
      </div>
      <form @submit.prevent="addType">
        <label class="text-[16px] font-medium" for="flowName">Type Name</label>
        <input
          type="text"
          id="typeName"
          v-model="typeName"
          placeholder="Enter name"
          class="w-full border rounded-md text-sm pt-4 mt-1 px-2 pb-2 mb-2 border-[#DDDEE2] outline-none"
        />
        <label class="text-[16px] font-medium" for="typeDescription"
          >Type Description</label
        >
        <textarea
          type="text"
          id="typeDescription"
          v-model="typeDescription"
          placeholder="Enter Description"
          class="w-full border rounded-md text-sm pt-4 mt-1 px-2 pb-2 mb-2 border-[#DDDEE2] outline-none"
        />
        <label class="text-[16px] font-medium" for="flowType">Type Hint</label>
        <textarea
          type="text"
          id="typeHint"
          v-model="typeHint"
          placeholder="Enter Hint"
          class="w-full border rounded-md text-sm pt-4 mt-1 px-2 pb-2 mb-2 border-[#DDDEE2] outline-none"
        />
        <button
          type="submit"
          class="bg-[#E6F9F0] text-[#09C269] rounded-lg text-sm font-medium w-fit p-3 mt-3"
        >
          Add Type
        </button>
      </form>
    </div>
  </q-dialog>
</template>

<script setup lang="ts">
defineProps({
  toggleLeftDrawer: Function,
});

import { supabase } from 'src/supabase';
import { ref, onMounted } from 'vue';
import { useToast } from 'vue-toastification';
import { useRoute } from 'vue-router';

interface Type {
  id: number;
  title: string;
  description: string;
  hint: string;
}

const toast = useToast();
const createFlow = ref(false);
const createType = ref(false);

const flowName = ref('');
const flowDescription = ref('');
const flowType = ref('');

const typeName = ref('');
const typeDescription = ref('');
const typeHint = ref('');
const route = useRoute();
const cardList = ref<Type[]>([]);

const addType = async () => {
  try {
    if (!typeName.value || !typeDescription.value || !typeHint.value) {
      toast.warning('Please fill all fields'); // just a simple validation
      return;
    }
    const toastId = toast.info('Adding type...', { id: 'adding-type-toast' });
    const res = await supabase.from('types').insert([
      {
        title: typeName.value,
        description: typeDescription.value,
        hint: typeHint.value,
      },
    ]);

    if (res?.error)
      throw res.error.details || 'An error occurred while adding the type';
    toast.dismiss(toastId);
    toast.success('Type added successfully');
  } catch (error) {
    toast.dismiss('adding-type-toast');
    toast.error(error);
  }
};

const addFlow = async () => {
  try {
    if (!flowName.value || !flowDescription.value || !flowType.value) {
      toast.warning('Please fill all fields');
      return;
    }
    const toastId = toast.info('Adding flow...', { id: 'adding-flow-toast' });
    const res = await supabase.from('flows').insert([
      {
        title: flowName.value,
        desc: flowDescription.value,
        type: flowType.value,
      },
    ]);

    if (res?.error)
      throw res.error.details || 'An error occurred while adding the flow';
    toast.dismiss(toastId);
    toast.success('Flow added successfully');
  } catch (error) {
    toast.dismiss('adding-flow-toast');
    toast.error(error);
  }
};

const fetchTypes = async () => {
  try {
    const res = await supabase.from('types').select('*');

    if (res.error) throw res.error.details || 'Error fetching types';

    cardList.value = res.data || [];
  } catch (error) {
    toast.dismiss('fetching-type-toast');
    toast.error(error);
  }
};

onMounted(() => {
  fetchTypes();
});
</script>
