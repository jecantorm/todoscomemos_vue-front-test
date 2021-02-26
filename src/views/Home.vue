<template>
  <div class="home">
    <Characters msg="Here will be the characters' cards"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
import Characters from '@/components/CharactersComponent.vue';

@Component({
  components: {
    HelloWorld,
    Characters
  },
})
export default class Home extends Vue {}
</script>
