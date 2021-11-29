<template>
  <div>
    
    <div v-for="post in post.postCollection.items" :key="post.title" class="mb-8">
       <!-- <p>{{$route.params.slug}}</p> -->
       <p><nuxt-link :to="'/news/'+post.slug">{{post.title}}</nuxt-link></p>
    </div> 
    <!-- <pre>{{planets}}</pre> -->
  </div>
</template>

<script>
import { gql } from 'nuxt-graphql-request'

export default {
  async asyncData({ $graphql, params }) {
    const query = gql`
      query post {
        postCollection {
          items {
            title
            slug
          }
        }
      }
    `;
    const post = await $graphql.default.request(query);
    //  console.log(planets);
    return { post };
  },
};
</script>
