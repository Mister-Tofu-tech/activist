<template>
  <div
    class="bg-light-layer-0 px-8 text-light-text dark:bg-dark-layer-0 dark:text-dark-text"
  >
    <Head>
      <Title>{{ $t("pages.events.index.header-title") }} </Title>
    </Head>
    <HeaderAppPage
      :header="$t('pages.events.index.header-title')"
      :tagline="$t('pages.events.index.subheader')"
    >
      <div class="flex flex-col space-x-3 sm:flex-row">
        <ShieldTopic topic="My topics dropdown" />
      </div>
    </HeaderAppPage>
    <div v-if="events">
      <div v-for="event in events" class="space-y-6 pb-6 pt-3 md:pt-4">
        <CardSearchResultEvent :isPrivate="false" :event="event" />
      </div>
    </div>
    <EmptyState v-else pageType="events" :permission="false" />
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: "sidebar",
});

const { data: events } = await useFetch(
  `${BASE_BACKEND_URL}/entities/organization_events/`,
  {
    method: "GET",
  }
);
</script>
