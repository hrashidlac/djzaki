<template>
  <div>
    <div v-for="mixtape in mixtapes.pageCollection.items" :key="mixtape.title" class="mb-8">
       <p><nuxt-link :to="mixtape.slug">{{mixtape.title}}</nuxt-link></p>
    </div> 
  </div>
</template>

<script>
import { gql } from 'nuxt-graphql-request'

export default {
  async asyncData({ $graphql, params }) {
    const query = gql`
      query mixtape { 
        pageCollection{
          items{
            title
            slug
          }
        }
      }
    `;
    const mixtapes = await $graphql.default.request(query);
    //  console.log(mixtapes);
    return { mixtapes };
  },
};
</script>
