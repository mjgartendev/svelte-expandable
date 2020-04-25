<script>
	//import {getContext} from 'svelte';
	//import {KEY} from './ExpandableGroup.svelte';

	import {onMount} from 'svelte';
	import Icon from 'mdi-svelte';
	import { mdiChevronLeft, mdiChevronRight, mdiArrowCollapse, mdiArrowExpand} from '@mdi/js';
	export let expanded = false;
	export let horizontal = false;
	export let right = false;
	export let heading = '';
	export let icon;
	function toggle() {
		expanded = !expanded;
	}
	function collapse(){
		panel.expanded = false;
	}
	function expand(){
		panel.expanded = true;
	}
	let panel;
	/* TODO: implement dynamic context registration to manage grouped panels
	const ctx = getContext(KEY);;
$: if(ctx) {
	expanded = panel === ctx.activePanel
}
	onMount(async() => {
		await ctx.addPanel(panel);
		console.log(ctx.panels)
		return () => ctx.removePanel(panel);
	})
	*/
	$: icon = () => {
		if(horizontal){
			if(right){
				return expanded ? mdiChevronRight : mdiChevronLeft;
			}else{
				return expanded ? mdiChevronLeft : mdiChevronRight;
			}
		}else{
			return expanded ? mdiArrowCollapse : mdiArrowExpand;
		}
	}
</script>

<section bind:this={panel} class:expanded class:horizontal class:right>
	<header on:click={toggle}>
		<slot name=heading {horizontal} {right} {expanded}>
			{#if horizontal}
			<p>{expanded ? heading : ''}</p>
			{:else}
			<p>{heading}</p>
			{/if}
			<Icon path={expanded ? mdiArrowCollapse : mdiArrowExpand}/>
		</slot>
	</header>
	{#if expanded}
	<div class="expandable">
		<slot></slot>
	</div>
	{/if}
</section>

<style>
	header {
		background: var(--header-bg, #edf2f7);
		height: var(--header-height, 32px);
		display: flex;
		align-items: center;
		justify-content: space-between;
		cursor:pointer;
		font-size: .8rem;
		text-transform: uppercase;
		border-bottom: 1px solid #fff;
		border-right: 1px solid #fff;
		padding: 0 8px;
		color: #5e84a0;
		font-weight: bold;
	}
	.expanded header {
		color: #295b82;
	}
	.right header {
		flex-direction: row-reverse
	}
	.horizontal{
		min-width: 40px;
		max-width: var(--sidebar-w, 150px);
		flex-direction: row;
	}
	.horizontal header {
		justify-content: center;
	}
	.horizontal.expanded header{
		justify-content: space-between;
	}
	.right{
		flex-direction: row-reverse;
	}
	.expandable {
		display: flex;
		flex-direction: column;
	}
	.expanded{
		height: 100%;
		width: 100%;
	}
</style>