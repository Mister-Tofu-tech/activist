<template>
  <div
    class="bg-light-layer-0 px-8 text-light-text dark:bg-dark-layer-0 dark:text-dark-text"
  >
    <Head>
      <Title>{{ $t("pages.organizations.index.header-title") }}</Title>
    </Head>
    <HeaderAppPage
      :header="$t('pages.organizations.index.header-title')"
      :tagline="$t('pages.organizations.index.subheader')"
    >
      <div class="flex flex-col space-x-3 sm:flex-row">
        <ComboboxTopics />
      </div>
    </HeaderAppPage>
    <div v-if="organizations">
      <div
        v-for="organization in organizations"
        class="space-y-6 pb-6 pt-3 md:pt-4"
      >
        <CardSearchResultOrganization
          :isPrivate="false"
          :organization="organization"
        />
      </div>
    </div>
    <EmptyState v-else pageType="organizations" :permission="false" />
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: "sidebar",
});

const { data: organizations } = await useFetch(
  `${BASE_BACKEND_URL}/entities/organizations/`,
  {
    method: "GET",
  }
);
</script>
