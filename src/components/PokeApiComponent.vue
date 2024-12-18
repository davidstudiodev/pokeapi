<template>
    <section class="bg-zinc-800 h-screen flex flex-col items-center p-20">
        <h1 class="text-2xl text-white p-10 flex text-center">Find you<br>Pokemon</h1>
        <div class="flex gap-5 flex-col md:flex-row">
            <input type="text" class="rounded-xl h-10 w-60 p-5 outline-none" placeholder="Write.." v-model="poke_input">
            <button class="bg-white p-2 rounded-xl w-24" @click="FindPokemon">Find</button>
        </div>
        <div class="text-white">
            <img class="bg-white h-48" :src="image" alt="">
            <div class="w-60 p-4">
                <h3 class="border">Name: {{ name }}</h3>
                <p class="border">Type: {{ type }}</p>
                <p class="border">Moves: {{ moves }}</p>
            </div>
        </div>

    </section>
  
</template>

<script>
export default {
name: 'PokeApi',
data() {
    return{
        poke_input: '',
        type: '',
        name: '',
        image: '',
        moves: '',
    }
},
methods: {
    FindPokemon(){
        fetch(`https://pokeapi.co/api/v2/pokemon/${this.poke_input}`)
        .then(res => res.json())
        .then(data => {
            this.image = data.sprites.front_default
            this.name = data.name
            this.type = data.types[Math.floor(Math.random() * data.types.length)].type.name
        })
    }
    
},
}
</script>

<style>

</style>