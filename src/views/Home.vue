<template>
  <div class="home">
    <h1>Home</h1>
    <Characters msg="hi"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Characters from '@/components/CharactersComponent.vue';

@Component({
  components: {
    Characters
  },
})
export default class Home extends Vue {}
</script>
