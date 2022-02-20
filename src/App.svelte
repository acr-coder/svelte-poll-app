<script>
	import Header from './components/Header.svelte'
	import Footer from './components/Footer.svelte'
	import PollList from './components/PollList.svelte'
	import Tabs from './shared/Tabs.svelte'
	import CreatePollForm from './components/CreatePollForm.svelte'

	let items = ['Current Survey', 'Add New Survey'];
	
	let activeItem = 'Current Survey';
	

	const tabChange = (e) => {
		activeItem = e.detail;
	}

	


	let polls = [
		{
			id:1,
			question: 'Python or Javascript?',
			answerA: 'Python',
			answerB: 'Javascript',
			votesA:9,
			votesB:15,
		},
	]

	const handleAdd = (e) => {
		const poll = e.detail;
		polls = [poll, ...polls];
		
		activeItem = 'Current Survey' 
	}

	const handleVote = (e) => {
		const { id, option } = e.detail;

		let copiedPolls = [...polls];
		let upvotedPoll = copiedPolls.find((poll) => poll.id == id);

		if (option === 'a'){
			upvotedPoll.votesA++;
		}
		if (option === 'b'){
			upvotedPoll.votesB++;
		}

		polls = copiedPolls;
	}
</script>

<Header  />
<main>
	<Tabs {items} {activeItem} on:tabChange={tabChange} />
	{#if activeItem === 'Current Survey' }
		<PollList {polls} on:vote={handleVote} />
	{:else if activeItem === 'Add New Survey' }
	<CreatePollForm on:add={handleAdd} />
	{/if}
	
</main>
<Footer />

<style>
	main{
		
		max-width: 960px;
		margin: 40px auto;
	}
	
	
</style>