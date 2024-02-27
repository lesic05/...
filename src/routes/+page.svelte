<script>
	import { supabase } from '$lib/supabase';

	let promise = supabase.from('countries').select();
	let countries = [];
</script>

<h1>Aufgaben:</h1>
<ul>
	<li>
		anstatt eines JS-Objekts, das auf der Seite dargestellt wird, möchte ich eine Liste aller Länder
	</li>
	<li>anstatt loading, loading spinner nehmen</li>
</ul>
{#await promise}
	<span class="loading loading-spinner loading-lg" />
{:then result}
	<div>{JSON.stringify(result)}</div>
{/await}

{#each countries as country}
	<div>
		<h2>{country.name}</h2>
	</div>
{/each}
