<template>
  <div>
    <div class="">
      <div class="mb-24">
        <div v-for="post in post.pageCollection.items" :key="post.title">
          <div>{{post.title}}</div>
          <div v-html="$md.render(post.body)"></div>
        </div> 
      </div>
    </div>
  </div>
</template>

<script>
import { gql } from 'nuxt-graphql-request'

export default {
  async asyncData({ $graphql }) {
    const query = gql`
      query  {
        pageCollection (where:  { slug: "welcome" }) {
          items {
            title
            slug
            body
            metaDescription
          }
        }
      }
    `
    
    const post = await $graphql.default.request(query)
    return { post  }
  },
};
</script>


