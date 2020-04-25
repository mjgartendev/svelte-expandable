<script>
	import Expandable from './Expandable.svelte';
	import ExpandableGroup from './ExpandableGroup.svelte';
</script> 

<div class="container">
	<ExpandableGroup orientation='vertical'>
		<ExpandableGroup orientation="horizontal">
			<Expandable expanded horizontal heading="Explorer">
				<p>horizontal</p>
			</Expandable>
			<ExpandableGroup orientation="vertical">
				<Expandable expanded heading='Input'>
					<p>1</p>
				</Expandable>
				<Expandable expanded heading='Output'>
					<p>2</p>
				</Expandable>
			</ExpandableGroup>
			<Expandable horizontal expanded right heading="Context">
				<p>horizontal</p>
				<p>right</p>
			</Expandable>
		</ExpandableGroup>
		<Expandable class="console" heading='Console'>
			<p>3</p>
		</Expandable>
	</ExpandableGroup>
</div>

<style>
	:global(*::before), :global(::after){
		box-sizing: inherit;
	}
	:global(body){
		box-sizing: border-box;
		padding: 0;
		height: 100vh;
		width: 100vw;
		overflow: hidden;
	}
	.container {
		width: 100vw;
		height: 100vh;
		display: grid;
		grid-template-rows: 1fr;
		grid-template-columns: 1fr;
	}
</style>

