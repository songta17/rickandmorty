<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        rickandmorty
      </h1>
      <div>
        <ul>
          <li v-for="character in characters.results" :key="character.id">
            {{ character.name }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'

import Logo from '~/components/Logo.vue'
export default {
  components: {
    Logo
  },
  // Step 2
  data() {
    return {
      characterId: 1
    }
  },
  apollo: {
    characters: gql`
      query getCharacters {
        characters {
          results {
            id
            name
          }
        }
      }
    `,
    character: {
      query: gql`
        query getCharacter($id: ID) {
          character(id: $id) {
            id
            name
          }
        }
      `,
      // Code before step 2
      // variables: {
      variables() {
        return {
          id: this.characterId
        }
      }
    }
  }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
