<script>
	export let expanded = true;
	export let heading = '';

	function toggle() {
		expanded = !expanded;
	}
</script>

<div class:expanded class="wrapper">
	<span on:click={toggle}>
		{heading}
	</span>
	{#if expanded}
		<slot {expanded}></slot>
	{/if}
</div>

<style>
	span {
		background: #f1f1f1;
		margin: 0;
		font-weight: bold;
		padding: .25rem 1rem;
		cursor: pointer;
	}
	.wrapper {
		display: flex;
		width: 100%;
		flex-direction: column;
		padding: 0;
		margin: 0;
		border: 1px solid #ccc;
		border-radius: 3px;
	}
	.expanded {
		height: 100%;
	}
</style>