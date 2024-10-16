<template>
  <q-layout view="lHh lpR lFf">
    <!-- <q-header elevated class=" q-display-md-none">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title> Quasar App </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header> -->
    <q-header class="bg-white">
      <TopBar :toggleLeftDrawer="toggleLeftDrawer" />
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-black px-2"
    >
      <div class="flex ml-6 mt-8 items-center gap-3">
        <LogoIcon />
        <span class="text-white text-base font-semibold">Mailrd</span>
      </div>

      <q-list class="mt-10">
        <EssentialLink
          v-for="link in linksList"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import EssentialLink from 'components/EssentialLink.vue';
import TopBar from 'components/TopBar.vue';
import HomeIcon from 'src/components/icons/HomeIcon.vue';
import CampaignIcon from 'src/components/icons/CampaignIcon.vue';
import FlowIcon from 'src/components/icons/FlowIcon.vue';
import PeopleIcon from 'src/components/icons/PeopleIcon.vue';
import ContentIcon from 'src/components/icons/ContentIcon.vue';
import ChatIcon from 'src/components/icons/ChatIcon.vue';
import LogoIcon from 'src/components/icons/LogoIcon.vue';

defineOptions({
  name: 'MainLayout',
});

const linksList = [
  {
    title: 'Home',
    icon: HomeIcon,
    link: '#',
  },
  {
    title: 'Campaigns',
    icon: CampaignIcon,
    link: '#',
  },
  {
    title: 'Flows',
    icon: FlowIcon,
    link: '/',
  },
  {
    title: 'Audience',
    icon: PeopleIcon,
    link: '#',
  },
  {
    title: 'Content',
    icon: ContentIcon,
    link: '#',
  },
  {
    title: 'Conversations',
    icon: ChatIcon,
    link: '#',
  },
];

const leftDrawerOpen = ref(false);

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}
</script>
