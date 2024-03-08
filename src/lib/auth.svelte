<script lang="ts">
	import { supabase } from '$lib/supabase';
	import { onMount } from 'svelte';
	import Notification from '$lib/Notification.svelte';
	let loading = false;
	let email = '';
	let showError = false;
	let errorMessage = '';

	const handleLogin = async () => {
		try {
			loading = true;
			showError = false;
			const { error } = await supabase.auth.signInWithOtp({ email });
			if (error) throw error;
		} catch (error) {
			if (error instanceof Error) {
				errorMessage = error.message;
				showError = true;
			}
		} finally {
			loading = false;
		}
	};
</script>

<Notification message={errorMessage} visible={showError} />
<div class="row flex-center flex">
	<div class="ml-64 mt-28 card w-1/3 bg-base-50 shadow-xl">
		<div class="card-body">
			<div class="col-6 form-widget" aria-live="polite">
				<h1 class=" my-10 header text-2xl">Supabase + Svelte</h1>
				<p class="mb-10 description text-xl">Sign in via magic link with your email below</p>
				<form class="form-widget" on:submit|preventDefault={handleLogin}>
					<div>
						<label for="email">Email</label>
						<input type="email" bind:value={email} placeholder="Enter your email" />
					</div>
				</form>
				<div class="card-actions justify-end">
					<button class="btn btn-outline" on:click={handleLogin} disabled={loading}
						>Send magic link!</button
					>
				</div>
			</div>

			<div />
		</div>
	</div>
</div>
