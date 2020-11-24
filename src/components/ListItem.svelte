<script>
	export let item;
	export let handleCompletion;
	export let handleDelete;
</script>

<li
	on:click={handleCompletion}
	id={item.id}
	class={item.completed ? 'completed' : null}>
	<span class="delete"><i on:click={handleDelete} class="fa fa-trash" /></span>
	{item.title.substring(0, 30)}{item.title.length > 30 ? '...' : ''}
	<span class="float-right view"><i class="fa fa-eye" /></span>
</li>
