<template>

  <div id="program">
      <h1>Program Component</h1>
        channelId: {{channelId}} <br>
        <input v-on:keydown.13="selectProgram" v-on:keydown.40.39="arrowSelect" v-on:keyup="searchPrograms" type="text" placeholder="Sök program" v-model="searchValue">

        <div id="results">
          <div v-on:click="selectProgram(program.id)" v-for="program in results" :key="program.id" :id="program.id">
            {{program.name}}
          </div>
        </div>
        <hr>
      <div class = "programs" v-for="program in programs" :key="program.id">
        <span>
           <img :src="program.programimage"> {{program.name}}
        </span>
      </div>

  </div>
</template>

<script>
import dataStore from '../store/dataStore';
export default {

  data:function(){
    return{
        programs:dataStore.data.programs,
        channelId:dataStore.data.channelId,
        results:[],
        searchValue:"",
        count:0
        }
      },
      created(){
        dataStore.methods.getPrograms();
          //console.table(this.programs);

      },
      methods:{

        searchPrograms(){
          this.results = this.programs.filter((program)=>{
            if(this.searchValue != "")
            {
              let r = program.name.toLowerCase().search(this.searchValue.toLowerCase());
              if(r != -1) return program.name;

            }
          });
        },
        arrowSelect(){
          
          let parent = document.getElementById("results");
          if(document.querySelector(".selected"))
          document.querySelector(".selected").classList.remove("selected");

          parent.children[this.count].classList.add("selected");
          this.count++;
          if(this.count>parent.children.length-1)
          {
            this.count = 0;
          }
        },
        selectProgram(id){
          alert(id);
          if(document.querySelector(".selected"))
          {
              const selected = document.querySelector(".selected").id;
              alert(selected);
          }
        }
      }
  

}
</script>


<style scoped>
img{
  height:40px;
  width:40px;
}
.programs span{
  cursor:pointer;
}
.selected{
  background: #303030;
  color:#fff;
}

</style>
