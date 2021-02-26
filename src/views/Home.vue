<template>
  <div class="home">
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
