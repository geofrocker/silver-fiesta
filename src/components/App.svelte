<script>
	import { fade } from "svelte/transition";
	import { v4 as uuidv4 } from "uuid";
	import ListItem from "./ListItem.svelte";
	import "../main.css";
	let data = [
		{
			id: uuidv4(),
			title: "Clean up assigned PR Queue",
			completed: false,
		},
		{
			id: uuidv4(),
			title: "Level up on serveless",
			completed: false,
		},
		{
			id: uuidv4(),
			title: "Visit Alpha",
			completed: false,
		},
	];
	let visible = false;

	const handleCompletion = (e) => {
		let tempData = data.map((item) => {
			if (item.id === e.target.id) {
				item.completed = !item.completed;
			}
			return item;
		});
		data = [...tempData];
	};

	const handleAdd = (e) => {
		if (e.which === 13 && e.target.value.length > 5) {
			let item = {
				id: uuidv4(),
				title: e.target.value,
				completed: false,
			};
			data.unshift(item);
			data = [...data];
			e.target.value = "";
		}
	};

	const handleDelete = (e) => {
		let id = e.target.parentNode.parentNode.id;
		let items = data.filter((item) => item.id != id);
		data = [...items];
	};
</script>

<main>
	<div id="container">
		<h1>
			To-Do List
			<i on:click={() => (visible = !visible)} class="fa fa-plus" />
		</h1>
		{#if visible}
			<input
				transition:fade
				on:keypress={handleAdd}
				type="text"
				placeholder="Add New Todo" />
		{/if}
		<ul>
			{#each data as item}
				<ListItem {item} {handleDelete} {handleCompletion} />
			{/each}
		</ul>
	</div>
</main>
