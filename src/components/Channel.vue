<template>
  <div id="channel">
    <h1>CHANNELS</h1>
     <div>
        <p v-for="id in favChannels" :key="id">
            {{id}}
        </p>
    </div>
    <div>
        <p v-for="channel in channels" :key="channel.id">
            <img @click="changeChannelId(channel.id)" :src="channel.image">
            {{channel.name}}
            <button @click="addFavChannel(channel.id)"> Add to favourites</button>
        </p>
    </div>
  </div>
</template>

<script>
import dataStore from "../store/dataStore.js"
export default {

    data:()=>{
        return{
            channels:[],
            favChannels:dataStore.data.favChannels
        }
    },
    methods:{
        addFavChannel(id)
        {
            dataStore.methods.addFavChannel(id);
        
        },
        changeChannelId(id){
            dataStore.methods.changeChannelId(id);
          // alert(id);
        }
    },
    async created(){
        const url = 'http://api.sr.se/api/v2/channels?format=json&pagination=false';
        const rawChan = await dataStore.methods.getData(url);
        this.channels = rawChan.channels;
    }
}
</script>

<style scoped>
    img{
        width:40px;
        height:40px;
    }

</style>