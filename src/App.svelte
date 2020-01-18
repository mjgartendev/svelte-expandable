<script>
	import Expandable from './Expandable.svelte';
	let script = '';
	let markup = '<p>Tomato!</p>';
	let style = 'p {\n\t\tcolor: tomato\n\t}';
	$: component = `<script>\n\t${script}\n<\/script>\n\n${markup}\n\n<style>\n\t${style}\n</style>`;
</script>

<style>
	:global(body){padding: 0}
	.container {
		display: flex;
	}
	section{
		display: flex;
		width: 100%;
		flex-direction: column;
	}
	div {
		height: 100%;
		border: 1px solid #ccc;
	}
	textarea{
		height: 100%;
		width: 100%;
		resize: none;
		background: #f6fafd;
	}
</style>
<div class="container">
	<section>
		<Expandable let:expanded heading='markup'>
			<div>
				{#if expanded}
				<textarea bind:value={markup}/>
				{/if}
			</div>
		</Expandable>
		<Expandable let:expanded heading='script'>
			<div>
				{#if expanded}
				<textarea bind:value={script}/>
				{/if}
			</div>
		</Expandable>
		<Expandable let:expanded heading='style'>
			<div>
				{#if expanded}
				<textarea bind:value={style}/>
				{/if}
			</div>
		</Expandable>
	</section>
	
	<section>
		<Expandable let:expanded expanded='true' heading='source'>
			<div>
				{#if expanded}
				<textarea bind:value={component}/>
				{/if}
			</div>
		</Expandable>
		<Expandable let:expanded expanded='true' heading='preview'>
			<div>
				{#if expanded}
				{@html component}
				{/if}
			</div>
		</Expandable>
	</section>
</div>