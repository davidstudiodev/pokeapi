<template>
    <section class="bg-zinc-800 h-screen flex flex-col items-center p-20">
        
        <img src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png" alt="">
        <h1 class="text-2xl text-white p-10 flex text-center">Find you<br>Pokemon</h1>
        
        <div class="flex items-center gap-5 flex-col md:flex-row">
            <input type="text" class="rounded-xl h-10 w-60 p-5 outline-none" placeholder="Write.." v-model="poke_input">
            <button class="bg-white p-2 rounded-xl w-24" @click="FindPokemon">Find</button>
        </div>
        
        <div class="text-white">
            <img class="border h-60 mt-10 w-60" :src="image" alt="">
            <div class="w-60 p-4 flex flex-col items-center">
                <h3 class="border p-2 w-60">Name: <strong class="text-yellow-300">{{ name }}</strong></h3>
                <p class="border p-2 w-60">Type: <strong class="text-green-300">{{ type }}</strong></p>
                <p class="border p-2 w-60">Moves: <strong class="text-blue-400">{{ moves }}</strong></p>
            </div>
        </div>

    </section>
  
</template>

<script>

import { useToast } from "vue-toastification";



export default {
name: 'PokeApi',
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

setup() {
    // Get toast interface
    const toast = useToast();

    // Use it!
    toast("I'm a toast!");

    // or with options
    toast.success("My toast content", {
        timeout: 2000
    });
    // These options will override the options defined in the "app.use" plugin registration for this specific toast

    // Make it available inside methods
    return { toast }
},
methods: {
    FindPokemon(){
        fetch(`https://pokeapi.co/api/v2/pokemon/${this.poke_input}`)
        .then(res => res.json())
        .then(data => {
            this.image = data.sprites.front_default
            this.name = data.name
            this.type = data.types[Math.floor(Math.random() * data.types.length)].type.name
            this.moves = data.moves[Math.floor(Math.random() * data.moves.length)].move.name
            this.showPoke = true
        })
    }
    
},
}
</script>

<style>

</style>