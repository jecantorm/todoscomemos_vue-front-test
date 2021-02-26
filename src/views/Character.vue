<template>
  <div class="character">
    <h1>Character</h1>
    <CharacterDetails msg="Here will be the character details"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import CharacterDetails from '@/components/CharacterDetailComponent.vue';

@Component({
  components: {
    CharacterDetails
  },
})
export default class Character extends Vue {}
</script>