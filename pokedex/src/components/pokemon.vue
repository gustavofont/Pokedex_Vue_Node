<template>
    <div class="pokemon">
        <div class="card">
            <div class="card-image">
                <figure>
                <img :src="currentImage" alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                <div class="media-content">
                    <p class="title is-4">{{num}} - {{pokemon.name | upper}}</p>
                    <p class="subtitle is-6">{{aboutPokemon.type}}</p>
                </div>
                </div>

                <div class="content">
                    <button @click="girarImg" class="button is-medium is-fullwidth">Girar Pokemon</button>
                </div>
            </div>
        </div>
    </div>
  
</template>

<script>
import axios from 'axios'

export default {
    created: function(){
        axios.get(this.pokemon.url).then(res => {
            this.aboutPokemon.type = res.data.types[0].type.name
            this.aboutPokemon.front = res.data.sprites.front_default
            this.aboutPokemon.back = res.data.sprites.back_default
            this.currentImage = this.aboutPokemon.front
        })
    },
    data(){
        return{
            isFront : true,
            currentImage : "",
            aboutPokemon: {
                type : "",
                front : "",
                back : ""
            }
        }
    },
    props:{
        pokemon: Object,
        num : Number
    },
    filters:{
        upper: function(ent){
            let newEnt = ent[0].toUpperCase() + ent.slice(1)
            return newEnt
        }
    },
    methods:{
        girarImg : function(){
            if(this.isFront){
                this.isFront = false
                this.currentImage = this.aboutPokemon.back
            }else{
                this.isFront = true
                this.currentImage = this.aboutPokemon.front
            }
        }
    } 
}
</script>

<style>
.pokemon{
    margin-top: 1%;
}
</style>