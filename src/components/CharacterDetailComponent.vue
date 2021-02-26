<template>
  <div class="character">
    <h1>{{ info.name }}</h1>
    <section v-if="errored">
      <p>There's nothing here</p>
    </section>
    <section v-else>
      <div v-if="loading">Loading...</div>
      <el-row v-else>
        <el-col :span="12" class="grid-content bg-purple-light" >
          <img :src="info.image"/>
        </el-col>
        <el-col :span="12">
          <h3>Created</h3>
          <p>{{ new Date(info.created).toDateString() }}</p>

          <h3>Species</h3>
          <p>{{ info.species }}</p>

          <h3>Type</h3>
          <p>{{ info.type}}</p>

          <h3>Gender</h3>
          <p>{{ info.gender }}</p>

          <h3>Origin Location</h3>
          <p>{{ info.origin.name }}</p>

          <h3>Current Location</h3>
          <p>{{ info.location.name }}</p>

          <h3>Status</h3>
          <p>{{ info.status}}</p>
          
        </el-col>
      </el-row>
    </section>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import axios from 'axios';

@Component
export default class CharacterDetails extends Vue {
  @Prop() private msg!: string;
  apiurl = 'https://rickandmortyapi.com/api/character/'
  charid = this.$route.params.id
  info: any = null
  errored = false
  loading = true

  mounted(){
    console.log("Character Mounted")
    const stringParameter = this.apiurl + this.charid
    console.log(stringParameter)
    this.doAPIPetition(stringParameter)
  }

  doAPIPetition(param: string){
    console.log(param)
    axios.get(param).then(response => {this.info = response.data})
    .catch(error => {
      console.log(error)
      this.errored = true
    })
    .finally(() => 
    this.loading = false)

  }


}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
  text-align:left;
}

h4{
  text-align: left;
}



img{
  width: 50%;
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

p {
  text-align: left;
}
</style>
