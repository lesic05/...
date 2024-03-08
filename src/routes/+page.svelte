<script>
	import { supabase } from '$lib/supabase';

	let promise = supabase.from('countries').select();
</script>

<div class="ml-64 mt-28 card w-1/2 bg-base-50 shadow-xl">
	<div class="card-body">
		<h1 class="p-20 text-4xl font-bold">Here we have a list of all the countries in the world!</h1>
		<h2 class="pl-20 text-2xl font-bold">Just click the button below:</h2>
		<div class="mx-40 my-16 collapse bg-base-200 w-auto justify-center align-middle">
			<input type="checkbox" />
			<div class=" collapse-title text-xl font-medium">
				<h1>COUNTRIES OF THE WORLD</h1>
			</div>
			<div class="collapse-content">
				{#await promise}
					<span class="loading loading-spinner loading-lg text-lg" />
				{:then result}
					{#each result.data as country}
						<p class="text-xl">{country.name}</p>
					{/each}
				{/await}
			</div>
		</div>
	</div>
</div>
