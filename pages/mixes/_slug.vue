<template>
  <div>
    <div v-for="mixtape in mixtape.mixtapeCollection.items" :key="mixtape.title">
       {{mixtape.title}}  
       <img :src="mixtape.heroImage.url" class="border p-2">       
       <vue-friendly-iframe :src="'https://www.mixcloud.com/widget/iframe/?hide_cover=1&mini=1&feed=%2Fdj-zaki%2F'+mixtape.mixcloudSlug +'%2F'" @load="onLoad"></vue-friendly-iframe>
    </div> 
    <!-- <pre>{{post}}</pre> -->
    <nuxt-link to="/mixes">Back</nuxt-link>
  </div>
</template>

<script>
import { gql } from 'nuxt-graphql-request'

export default {
  async asyncData({ $graphql, params }) {
    const query = gql`
      query ($name: String) {
        mixtapeCollection (where:  { slug: $name }) {
          items {
            slug
            title
            mixcloudSlug
            heroImage{
              fileName
              url(transform: {width: 500, height: 350})
            }
          }
        }
      }
    `
    
    const variables = { name: params.slug } 
    const mixtape = await $graphql.default.request(query, variables)
    console.log(mixtape.mixtapeCollection);
    return { mixtape }
  },
};
</script>
