<template>
  <div>
    <div class="">
      <div class="mb-24">
        <div v-for="post in post.pageCollection.items" :key="post.title">
          <div>{{post.title}}</div>
          <div v-html="$md.render(post.body)"></div>
        </div> 
      </div>
      <div class="grid grid-cols-3 gap-12">
        <div v-for="mixtape in mixtape.mixtapeCollection.items" :key="mixtape.title">
          <nuxt-link :to="'mixes/'+mixtape.slug">
            <div>{{mixtape.title}}</div>
            <img :src="mixtape.heroImage.url" class="border p-2 w-48">
          </nuxt-link>
        </div> 
        <!-- <pre>{{post}}</pre> -->
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
    const mixtapes = gql`
      query  {
        mixtapeCollection {
          items {
            title
            slug
            heroImage{
              fileName
              url(transform: {width: 500, height: 350})
            }
          }
        }
      }
    `
    const post = await $graphql.default.request(query)
    const mixtape = await $graphql.default.request(mixtapes)
    return { post, mixtape  }
  },
};
</script>


