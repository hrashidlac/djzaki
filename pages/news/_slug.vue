<template>
  <div>
    <div v-for="post in post.postCollection.items" :key="post.title">
       {{post.title}}
       <img :src="post.heroImage.url" class="border p-8">
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
        postCollection (where:  { slug: $name }) {
          items {
            slug
            title
            playlist
            heroImage{
              fileName
              url(transform: {width: 500, height: 350})
            }
          }
        }
      }
    `
    
    const variables = { name: params.slug } 
    const post = await $graphql.default.request(query, variables)
    console.log(post.postCollection);
    return { post }
  },
};
</script>
