<template>
    <div class="container">
        <div class="card text-center align-middle ">
           <figure class="figure card-img-top">
             <img :src="currentImg" alt="Foto pokemon" class="figure-img pt-5">
           </figure>
            <div class="card-body">
                <h2 class="card-title">{{ num +"-"+upperName}}</h2>
                <div>
                    <p class="card-text">{{pokemon.type}}</p>
                    <button class="btn btn-success" @click="mudarSprite">Sprite</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    created:async function(){
        try{
            let res = await axios.get(this.url)
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front
        }catch(err){
            console.log(err)
        }
    },
    data(){
        return{
            isFront: true,
            currentImg:"",
            pokemon:{
                
                type:"",
                front:'',
                back:''
                
            }
        }
    },
    props:{
        num:Number,
        name:String,
        url:String,
    },
    computed:{
        upperName:function(){
            return this.name[0].toUpperCase() + this.name.substring(1)
        }
    },
    methods:{
        mudarSprite:function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back
            }else{
                this.isFront = true;
                this.currentImg = this.pokemon.front
            }
        }
    }
}
</script>

<style scoped>

</style>