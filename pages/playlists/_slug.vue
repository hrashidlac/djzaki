<template>
  <div>
    <div v-for="post in post.spotifyPlaylistCollection.items" :key="post.title">
       <div>{{post.title}}</div>
       <div>{{post.body}}</div>
       <div></div>
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
        spotifyPlaylistCollection (where:  { slug: $name }) {
          items {
            slug
            title  
            body
            spotifyUrl
          }
        }
      }
    `
    
    const variables = { name: params.slug } 
    const post = await $graphql.default.request(query, variables)
    console.log(post.faqsCollection);
    return { post }
  },
};
</script>
