<template>
  <b-container>
    <ProfileOverview :profiles="profiles" :categories="categories" :type="type" />
  </b-container>
</template>

<script>
import { createClient } from '~/plugins/contentful.js'
const client = createClient()

export default {
  async asyncData ({ env, params: { type } }) {
    const { items: profiles } = await client.getEntries({
      content_type: 'profile',
      order: 'fields.name',
      'fields.type': type
    })
    const { items: categories } = await client.getEntries({
      content_type: 'category',
      'fields.type': type
    })

    return {
      profiles,
      categories,
      type
    }
  }
}
</script>
