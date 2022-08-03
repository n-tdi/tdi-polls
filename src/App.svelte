<script>
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';
	import PollList from './components/PollList.svelte';
	import Tabs from './shared/Tabs.svelte';
	import CreatePoleForm from './components/CreatePoleForm.svelte';
	
	// Tabs
	let items = ['Current Polls', 'Add New Poll'];
	let activeItem = items[0];
	const tabChange = (e) => {
		activeItem = e.detail;
	};

	// Polls
	let polls = [
		{
			id: 1,
			question: 'Python or JavaScript?',
			answerA: 'Python',
			answerB: 'JavaScript',
			votesA: 9,
			votesB: 15,
		},
  	];
	const handleAdd = (e) => {
		const poll = e.detail;
		polls = [poll, ...polls];
		activeItem = items[0];
		console.log(polls);
	};

	const handleVote = (e) => {
		const {option, id} = e.detail;
		let copPolls = [...polls]; // Capybara: Ok I pull up... ...the polls array and make a copy of it.
		const poll = copPolls.find(p => p.id === id);
		if (option === 'a') {
			poll.votesA++;
		} else {
			poll.votesB++;
		}
		polls = [...copPolls];
	};
</script>

<Header />
<main>
	<Tabs {items} {activeItem} on:tabChange={tabChange}/>
	{#if activeItem === items[0]}
		<PollList {polls} on:vote={handleVote}/>
	{:else if activeItem === items[1]}
		<CreatePoleForm on:addPoll={handleAdd} />
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