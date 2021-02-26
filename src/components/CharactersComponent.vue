<template>
  <div class="characters">
    <h1> Rick and Morty Characters </h1>
    <h2> Search a character </h2>
    <el-row>
      <form class="search-form" @submit="onSubmit">
        <el-col :span="4">
          <label for="name">Name: </label>
          <input id="name" v-model="ch_name" placeholder="Enter Name">
        </el-col>
        <el-col :span="4">
          <label for="status">Status: </label>
          <select id="status" v-model="ch_status">
            <option>alive</option>
            <option>death</option>
            <option>unknown</option>
          </select>
        </el-col>
        <el-col :span="4">
          <label for="species">Species: </label>
          <input id="species" v-model="ch_species" placeholder="Enter Species">
        </el-col>
        <el-col :span="4">
          <label for="type">Type: </label>
          <input id="type" v-model="ch_type" placeholder="Enter Type">
        </el-col>
        <el-col :span="4">
          <label for="gender">Gender: </label>
          <select id="gender" v-model="ch_gender">
            <option>female</option>
            <option>male</option>
            <option>genderless</option>
            <option>unknown</option>
          </select>
        </el-col>
        <el-col :span="4">
          <button type="submit">
            Search
          </button>
        </el-col>
      </form>
    </el-row>
    <h2> List of characters </h2>
    <section v-if="errored">
      <p>There's nothing here</p>
    </section>
    <section v-else>
      <div v-if="loading">Loading...</div>
    
      <el-row v-else>
        <el-col :span="6" v-for="character in info.results" :key="character.id" class="character">
          <el-card :body-style="{ padding: '0px' }" @click.native="onCardClicked(character.id,character.name)">
            <img :src="character.image"/>
            <div style="padding: 14px;">
              <span>
              {{ character.name }}
              </span>
            </div>
          </el-card>
        </el-col>
      </el-row>
    </section>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import axios from 'axios';

@Component
export default class Characters extends Vue {
  @Prop() private msg!: string;
  apiurl = 'https://rickandmortyapi.com/api/character'
  info: any = null
  errored = false
  loading = true

  //Character Search Info
  ch_name = ""
  ch_status = ""
  ch_species = ""
  ch_type = ""
  ch_gender = ""

  mounted(){
    console.log("mounted")
    this.doAPIPetition(this.apiurl)
  }

  onSubmit(){
    console.log("onSubmit")
    const stringParameter = this.apiurl + "/?" + "name=" + this.ch_name + "&status=" + this.ch_status + "&species=" + this.ch_species + "&type=" + this.ch_type + "&gender=" + this.ch_gender;
    this.doAPIPetition(stringParameter)
    
  }

  onCardClicked(pid: any, pname: any){
    console.log(pid)
    const routeData = this.$router.resolve({name: "Character", params: {id: pid, name: pname} })
    window.open(routeData.href, '_blank')
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
}

h2 {
  text-align:left;
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
