<script>
	import { supabase } from '$lib/supabase';

	let promise = supabase.from('countries').select();
	let countries = [supabase.from('countries').select('name')];
</script>

{#await promise}
	<span class="loading loading-spinner loading-lg" />
{:then result}
	{#each result.data as country}
		<p>{country.name}</p>
	{/each}
{/await}
