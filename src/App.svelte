<script>
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';
	import Tabs from './shared/Tabs.svelte';
	import CreatePoleForm from './components/CreatePoleForm.svelte';
	
	// Tabs
	let items = ['Current Polls', 'Add New Poll'];
	let activeItem = items[0];
	const tabChange = (e) => {
		activeItem = e.detail;
	}
</script>

<Header />
<main>
	<Tabs {items} {activeItem} on:tabChange={tabChange}/>
	{#if activeItem === items[0]}
		<p>Current Polls</p>
	{:else if activeItem === items[1]}
		<CreatePoleForm />
	{:else}
		<p>Nani?!?</p>
	{/if}
</main>
<Footer />

<style>
	main {
		max-width: 65%;
		margin: 0 auto;
	}
</style>