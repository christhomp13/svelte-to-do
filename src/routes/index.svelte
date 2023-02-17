<script>
    import { pokemon } from "../stores/pokestore";
    import PokemanCard from "../components/pokemanCard.svelte"
    
    let searchTerm = ""
    let filteredPokemon = [];

    //reacts to any data that changes that is referenced
    $: {
        if(searchTerm){
            filteredPokemon = $pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase()))
        }else{
            filteredPokemon=[...$pokemon]
        }
    }
</script>

<svelte:head>
    <title>Pokedex</title>
</svelte:head>

<h1 class='text-5xl text-center my-8 uppercase'>Pokedex</h1>

<input class="w-full rounded-md text-lg p-4 border-2 border-gray-200" type="text" placeholder="Search Pokemon" bind:value={searchTerm}>

<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1">
    {#each filteredPokemon as pokeman}
        <PokemanCard pokeman={pokeman}/> 
    {/each}
</div>


