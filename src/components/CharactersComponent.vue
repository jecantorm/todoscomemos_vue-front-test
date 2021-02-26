<template>
  <div class="characters">
    <h1> Rick and Morty Characters </h1>
    <h2> Search a character </h2>
    <el-row>
      <el-form :inline="true" class="search-form">
          <el-form-item label="Name">
          <el-input v-model="ch_name" placeholder="Enter Name"></el-input>
          </el-form-item>

          <!--el-form-item label="Status">
          <el-select v-model="ch_status" placeholder="Select Status">
            <el-option>alive</el-option>
            <el-option>death</el-option>
            <el-option>unknown</el-option>
          </el-select>
          </el-form-item-->
          <el-form-item label="Status">
          <el-input v-model="ch_status" placeholder="Options:[alive,dead,unknown]"></el-input>
          </el-form-item>
         
        
          <el-form-item label="Species">
          <el-input v-model="ch_species" placeholder="Enter Species"></el-input>
          </el-form-item>
        
          <el-form-item label="Type">
          <el-input v-model="ch_type" placeholder="Enter Type"></el-input>
          </el-form-item>
        
          <!--el-form-item label="Gender">
          <el-select v-model="ch_gender" placeholder="Select Gender">
            <el-option>female</el-option>
            <el-option>male</el-option>
            <el-option>genderless</el-option>
            <el-option>unknown</el-option>
          </el-select>
          </el-form-item-->

          <el-form-item label="Gender">
            <el-input v-model="ch_gender" placeholder="Options: [female,male,genderless,unknown]"></el-input>
          </el-form-item>
        
          <el-button type="primary" @click="onSubmit">
            Search
          </el-button>
      </el-form>
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
