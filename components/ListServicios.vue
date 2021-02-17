<template>
  <div>
    <div>Locale: {{$i18n.locale}}</div>
    <div
      v-for="service in services"
      :key="service.ID"
    >
      <div>
        {{ service.post_title }}
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  async fetch() {
    await this.loadServices()
  },
  data: () => ({
    services: [],
  }),
  methods: {
    async loadServices() {
      try {
        // @ts-ignore
        this.services = await this.$content(this.$i18n.locale === 'es' ? 'servicios' : 'en/services', {
          deep: true,
        })
        .fetch()
      } catch (e) {}
    },
  },
})
</script>
