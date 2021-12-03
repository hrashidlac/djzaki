<template>
  <div>s
    <div v-for="post in post.pageCollection.items" :key="post.title">
       <div>{{post.title}}</div>
    </div> 
    <!-- <pre>{{post}}</pre> -->
  </div>
</template>

<script>
import { gql } from 'nuxt-graphql-request'

export default {
  async asyncData({ $graphql, params }) {
    const query = gql`
      query ($name: String) {
        pageCollection (where:  { slug: $name }) {
          items {
            title
            slug
            body
            metaDescription
          }
        }
      }
    `
    
    const variables = { name: params.slug } 
    const post = await $graphql.default.request(query, variables)
    console.log(post.pageCollection);
    return { post }
  },
};
</script>
