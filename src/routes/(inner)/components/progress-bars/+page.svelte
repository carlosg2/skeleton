<script lang="ts">
	import DocsShell from '$docs/layouts/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings } from '$docs/layouts/DocsShell/types';
	import DocsPreview from '$docs/components/DocsPreview/DocsPreview.svelte';
	// Components
	import ProgressBar from '$lib/components/ProgressBar/ProgressBar.svelte';
	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';
	// Sveld
	import sveldProgressBar from '$lib/components/ProgressBar/ProgressBar.svelte?raw&sveld';

	// Defaults
	const defaultRounded = 'rounded-token';
	const defaultMeter = 'bg-surface-900-50-token';
	const defaultTrack = 'bg-surface-200-700-token';

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Component,
		name: 'Progress Bars',
		description: 'An indicator showing the progress or completion of a task.',
		imports: ['ProgressBar'],
		source: 'components/ProgressBar',
		aria: 'https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/progressbar_role',
		components: [{ sveld: sveldProgressBar }]
	};

	// Reactive Props
	$: props = {
		determinate: true,
		value: 50,
		max: 100,
		step: 10,
		height: 'h-2',
		rounded: defaultRounded,
		meter: defaultMeter,
		track: defaultTrack
	};
</script>

<DocsShell {settings}>
	<!-- Slot: Sandbox -->
	<svelte:fragment slot="sandbox">
		<DocsPreview>
			<svelte:fragment slot="preview">
				<ProgressBar label="Progress Bar" bind:value={props.value} max={props.max} />
			</svelte:fragment>
			<svelte:fragment slot="footer">
				<div class="w-48 mx-auto"><input type="range" min="0" bind:value={props.value} max={props.max} step={props.step} /></div>
			</svelte:fragment>
			<svelte:fragment slot="source">
				<CodeBlock language="html" code={`<ProgressBar label="Progress Bar" value={${props.value}} max={${props.max}} />`} />
			</svelte:fragment>
		</DocsPreview>
	</svelte:fragment>

	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<section class="space-y-4">
			<h2>Indeterminate Mode</h2>
			<p>Remove the <code>value</code> property or set value to <code>undefined</code>.</p>
			<DocsPreview background="neutral">
				<svelte:fragment slot="preview">
					<ProgressBar />
				</svelte:fragment>
				<svelte:fragment slot="source">
					<CodeBlock language="html" code={`<ProgressBar />`} />
					<CodeBlock language="html" code={`<ProgressBar value={undefined} />`} />
				</svelte:fragment>
			</DocsPreview>
		</section>
		<section class="space-y-4">
			<h2>Native Alternative</h2>
			<p>The native <code>progress</code> element works cross browser, but does not currently support Indeterminate mode when styled.</p>
			<DocsPreview background="neutral">
				<svelte:fragment slot="preview">
					<progress value={props.value} max={props.max} />
				</svelte:fragment>
				<svelte:fragment slot="source">
					<CodeBlock language="html" code={`<progress value={props.value} max={props.max} />`} />
				</svelte:fragment>
			</DocsPreview>
		</section>
		<hr />
		<section class="space-y-4">
			<h2>Accessibility</h2>
			<!-- prettier-ignore -->
			<p>
				This component is treated as an <a href="https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/progressbar_role" target="_blank" rel="noreferrer">ARIA progressbar</a>.
			</p>
		</section>
	</svelte:fragment>
</DocsShell>
