<template>
    <section class="bg-zinc-800 h-screen flex flex-col items-center p-5">
        
        <img class="w-44 md:w-96 md:p-10" src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png" alt="">
        <h1 class="text-2xl text-white pt-5 pb-2 flex text-center w-screen justify-center">Find your Pokemon</h1>
        
        <div class="flex items-center gap-2 flex-col md:flex-row md:p-8">
            <input type="text" class="rounded-xl h-10 w-50 p-5 outline-none md:w-96 md:h-16" placeholder="Write.." v-model="poke_input">
            <button class="bg-green-400 font-bold cursor-pointer p-2 rounded-xl w-24 md:w-32 md:h-16" @click="FindPokemon">Find</button>
        </div>
        
        <div class="text-white md:flex flex-row gap-10 md:p-5">
            <img class="border h-60 mt-5 w-60 bg-yellow-400 animate__animated animate__bounce" :src="image" alt="">
            <div class="w-60 p-4 flex flex-col items-center md:w-80 md:flex md:justify-center">
                <h3 class="border p-2 w-60 md:h-20 md:flex md:items-center md:w-80 md:text-xl">Name: <strong class="text-yellow-300">{{ name }}</strong></h3>
                <p class="border p-2 w-60 md:h-20 md:flex md:items-center md:w-80 md:text-xl">Type: <strong class="text-green-300">{{ type }}</strong></p>
                <p class="border p-2 w-60 md:h-20 md:flex md:items-center md:w-80 md:text-xl">Moves: <strong class="text-blue-400">{{ moves }}</strong></p>
            </div>
        </div>

    </section>
  
</template>

<script>

import { useToast } from "vue-toastification";



export default {
name: 'PokeApi',

setup() {
    // Get toast interface
    const toast = useToast();
    return { toast }    
},

data() {
    return{
        poke_input: '',
        type: '',
        name: '',
        image: '',
        moves: '',
        showPoke: false,
        
    }
},

methods: {
    FindPokemon(){
        
        if (!this.poke_input.trim()) {
                this.toast.error('Please enter a valid Pokémon name!', {
                    position: 'bottom-center',
                });
                return;
        }


        fetch(`https://pokeapi.co/api/v2/pokemon/${this.poke_input}`)
        .then(res => res.json())
        .then(data => {
            this.image = data.sprites.front_default
            this.name = data.name
            this.type = data.types[Math.floor(Math.random() * data.types.length)].type.name
            this.moves = data.moves[Math.floor(Math.random() * data.moves.length)].move.name
            this.showPoke = true
            this.poke_input = ''
    
        })
    
    .catch(() => {
        this.toast.error('Something went wrong! Pokémon not found.', 
        {position: 'bottom-center'
        })
        this.showPoke = false
        this.poke_input = ''
    })    

    }
    
},
}
</script>

<style>

</style>