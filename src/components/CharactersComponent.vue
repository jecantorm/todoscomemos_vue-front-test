<template>
  <div class="characters">
    <h1> Rick and Morty Characters </h1>
    <el-row>
      <el-col :span="6" v-for="character in info.results" :key="character.id" class="character">
        <el-card :body-style="{ padding: '0px' }">
          <img :src="character.image"/>
          <div style="padding: 14px;">
            <span>
            {{ character.name }}
            </span>
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import axios from 'axios';

@Component
export default class Characters extends Vue {
  @Prop() private msg!: string;
  api_url = 'https://rickandmortyapi.com/api/character'
  info: any = null
  errored = false
  loading = true

  mounted(){
    console.log("mounted")
    axios.get(this.api_url).then(response => {this.info = response.data})
    .catch(error => {
      console.log(error)
      this.errored = true
    })
    .finally(() => this.loading = false)
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

</style>
