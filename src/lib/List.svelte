<script lang="ts">
import { onMount } from "svelte";

    let d = [];
    let copy = [];

    function handleChange(e) {
		let filtered = d.filter(a => a.name.includes(e.target.value));
        console.log(filtered);
        if(filtered.length) {
            d = filtered
        } else d = copy;
	}


onMount(async () => {
  fetch("https://pokeapi.co/api/v2/pokemon")
  .then(response => response.json())
  .then(data => {
    console.log(data);
	d = data.results;
    copy = data.results;
  }).catch(error => {
    console.log(error);
    return [];
  });
});
</script>



 <input
	placeholder="Type some gibberish here"
	on:input={handleChange}
>

    <ul>
	{#each d as x}
		<li>{x.name}</li>
    {:else}
    	<!-- this block renders when photos.length === 0 -->
		<p>loading...</p>
	{/each}

</ul>

 
