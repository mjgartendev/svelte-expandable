<script context=module>
	export const KEY = {}
</script>
<script>
	import {setContext} from 'svelte';
	export let orientation = 'vertical';
		const context = {
		activePanel: '',
		isAccordion: true,
		minExpanded: 1,
		maxExpanded: 1
	};
	const panels = new Set();
	export const addPanel = panel => panels.add(panel);
	export const selectPanel = panel => {
		context.activePanel.collapse();
		context.activePanel = panels.get(panel);
	};
	export const removePanel = panel => panels.delete(panel);
	export const collapseAll = () => panels.forEach(panel => panel.collapse());
	export const expandAll = () => panels.forEach(panel => panel.expand());
	export const accordionManager = {
		panels, selectPanel, addPanel, removePanel, context, collapseAll, expandAll
	}
	setContext(KEY, {
		panels,
		addPanel,
		selectPanel,
		removePanel,
		activePanel: context.activePanel
	})
</script>

<section class={orientation === 'vertical' ? 'vertical' : 'horizontal'}>
	<slot {orientation} {accordionManager}/>
</section>

<style>	
	section{
		display: flex;
		height: 100%;
		width: 100%;
		flex-direction: column;
		border: 1px solid #edf2f7;
	}
	.horizontal {
		flex-direction: row;
	}
	.vertical {
		flex-direction: column;
	}
</style>