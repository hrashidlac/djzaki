<template>
  <div>
    
    <div v-for="faq in faq.spotifyPlaylistCollection.items" :key="faq.title" class="mb-8">
       <!-- <p>{{$route.params.slug}}</p> -->
       <p><nuxt-link :to="'/playlists/'+faq.slug">{{faq.title}}</nuxt-link></p>
    </div> 
    <!-- <pre>{{planets}}</pre> -->
  </div>
</template>

<script>
import { gql } from 'nuxt-graphql-request'

export default {
  async asyncData({ $graphql, params }) {
    const query = gql`
      query faq {
        spotifyPlaylistCollection {
          items {
            title
            slug
          }
        }
      }
    `;
    const faq = await $graphql.default.request(query);
    //  console.log(planets);
    return { faq };
  },
};
</script>
