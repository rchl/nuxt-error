<template>
  <div>
    <component :is="template" v-if="template !== ''" :post="post"></component>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Post } from '~/types/types'
import TemplateHome from '~/components/templates/TemplateHome.vue'

export default Vue.extend({
  components: {
    TemplateHome,
  },
  // @ts-ignore
  // eslint-disable-next-line prettier/prettier
  async asyncData({ $content, params, app: { i18n: { locale } } }) {
    let path = '/' + params.pathMatch

    if (params.pathMatch === '') {
      // home
      path = locale === 'es' ? '/index' : `/${locale}`
    } else if (locale !== 'es') {
      path = `/${locale}${path}`
    }

    // @ts-ignore
    const [post] = await $content({ deep: true }).where({ path }).fetch()

    return { post, template: 'TemplateHome' }
  },
  data: () => ({
    post: {} as Post,
    template: '',
    textMouse: '',
  }),
})
</script>
