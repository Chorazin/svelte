<script>
import Modal from './modal.svelte';
import Add_Person_Form from './Add_Person_Form.svelte';

	let people = [
		{ name: 'Harry Kane', position: 'striker', age: 26, id: 1 },
		{ name: 'Dele Alli', position: 'midfielder', age: 24, id: 2 },
		{ name: 'Son Heung Min', position: 'wide forward', age: 28, id: 3 },
		{ name: 'Moussa Sissoko', position: 'midfielder', age: 30, id: 4 }
	]
	let show_modal = false;
	const delete_player = (id) => {
		//delete player clicked
		console.log(id);
		return() => {
			people = people.filter((player) => player.id != id);
		};
	};

	const modal_toggle = () => {
		show_modal = !show_modal;
	};

	const add_person = (e) => {
		const person = e.detail;
		people = [person, ...people];
		show_modal = false;
	};

</script>

<Modal show_modal={show_modal} on:click={modal_toggle}>
	<Add_Person_Form on:add_person_event={add_person} />
</Modal>
<main>
  <button on:click={modal_toggle}>open modal</button>
	{#each people as player (player.id)}
		<div>
			<h4>player: {player.name}</h4>
			<p>age: {player.age}</p>
			{#if player.position === 'midfielder'}
				<p>Zidane wannabe</p>
			{/if}
			<p>position: {player.position}</p>
			<button on:click={delete_player(player.id)}>delete player</button>
		</div>
	{:else}
		<p>There are no players to show</p>
	{/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
