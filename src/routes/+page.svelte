<script lang="ts">
	// src/routes/+page.svelte

	const { data } = $props();
	const supabase = data.supabase;
	const session = data.session;
	const isLoggedIn = session?.user ? true : false;

	async function loginWithGoogle() {
		const data = await supabase.auth.signInWithOAuth({
			provider: 'google'
		});
		console.log(data);
	}

	async function logout() {
		const data = await supabase.auth.signOut();
		// TODO: need to refresh the page to see the changes
		console.log(data);
	}
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>

{#if isLoggedIn}
	<p>Welcome {session?.user?.email}</p>
	<button onclick={logout}>Logout</button>
{:else}
	<button onclick={loginWithGoogle}>Login with Google</button>
{/if}
