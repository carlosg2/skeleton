<script lang="ts">
	import DocsShell from '$docs/layouts/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings } from '$docs/layouts/DocsShell/types';
	import DocsPreview from '$docs/components/DocsPreview/DocsPreview.svelte';
	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Element,
		name: 'Core',
		description: 'Provides a variety of globally scoped styles.',
		stylesheetIncludes: ['all', 'core'],
		source: 'styles/core.css'
	};
</script>

<DocsShell {settings}>
	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<!-- Body -->
		<div class="space-y-4">
			<h2>Body Background</h2>
			<p>
				Your app's background is automatically set via a <a href="https://www.skeleton.dev/elements/tokens" target="_blank" rel="noreferrer"
					>design token</a
				> class. Adjust your theme's color scheme to customize. This affects both light and dark mode.
			</p>
			<CodeBlock language="css" code={`body { @apply bg-surface-50-900-token; }`} />
			<aside class="alert variant-ghost-warning">
				<i class="fa-solid fa-lightbulb text-2xl" />
				<div class="alert-message">Consider pairing this with a <strong>CSS Mesh Gradient</strong> or other background image.</div>
				<div class="alert-actions">
					<!-- prettier-ignore -->
					<a class="btn variant-ghost-warning" href="https://github.com/skeletonlabs/skeleton/blob/master/src/lib/themes/theme-skeleton.css#L115" target="_blank" rel="noreferrer">Reference</a>
					<a class="btn variant-filled" href="https://csshero.org/mesher/" target="_blank" rel="noreferrer">Mesh Generator</a>
				</div>
			</aside>
		</div>
		<!-- Selection -->
		<div class="space-y-4">
			<h2>Selection</h2>
			<p>
				Selection color is also set via a token class. Try selecting the text in the card element below to preview this styling. Notice how
				selection color changes depending on the background.
			</p>
			<DocsPreview background="neutral">
				<svelte:fragment slot="preview">
					<p>The quick brown fox jumps over the lazy dog.</p>
				</svelte:fragment>
				<svelte:fragment slot="footer">
					<p class="w-full text-center">Try selecting the text above.</p>
				</svelte:fragment>
				<svelte:fragment slot="source">
					<CodeBlock language="css" code={`::selection { @apply bg-primary-500/30; }`} />
				</svelte:fragment>
			</DocsPreview>
		</div>
		<!-- Mobile Focus -->
		<div class="space-y-4">
			<h2>Mobile Focus</h2>
			<p>
				Interactive elements on mobile will briefly show a <a
					href="https://developer.mozilla.org/en-US/docs/Web/CSS/:focus"
					target="_blank"
					rel="noreferrer"><code>focus</code></a
				> style when touched. Skeleton adjusts the coloring.
			</p>
			<DocsPreview background="neutral">
				<svelte:fragment slot="preview">
					<button class="btn variant-soft">Tap Me</button>
				</svelte:fragment>
				<svelte:fragment slot="source">
					<CodeBlock language="css" code={`html { -webkit-tap-highlight-color: rgba(128, 128, 128, 0.5); }`} />
				</svelte:fragment>
			</DocsPreview>
		</div>
		<!-- Scrollbars -->
		<div class="space-y-4">
			<h2>Scrollbars</h2>
			<p>
				Skeleton automatically provides custom scrollbar styles in supported browsers. Use <code>.hide-scrollbar</code> to disable scrollbars.
			</p>
			<DocsPreview background="neutral">
				<svelte:fragment slot="preview">
					<div class="card p-4 max-h-[200px] overflow-auto space-y-4">
						<h3 data-toc-ignore>Test Scrolling Here</h3>
						<p>
							Lorem ipsum, dolor sit amet consectetur adipisicing elit. Culpa corrupti iusto dolor. Similique quibusdam eveniet quae
							deleniti architecto modi natus, quos ducimus! Repudiandae reiciendis totam sequi veniam necessitatibus, magni harum. Lorem
							ipsum, dolor sit amet consectetur adipisicing elit. Culpa corrupti iusto dolor. Similique quibusdam eveniet quae deleniti
							architecto modi natus, quos ducimus! Repudiandae reiciendis totam sequi veniam necessitatibus, magni harum. Lorem ipsum, dolor
							sit amet consectetur adipisicing elit. Culpa corrupti iusto dolor. Similique quibusdam eveniet quae deleniti architecto modi
							natus, quos ducimus! Repudiandae reiciendis totam sequi veniam necessitatibus, magni harum. Lorem ipsum, dolor sit amet
							consectetur adipisicing elit. Culpa corrupti iusto dolor. Similique quibusdam eveniet quae deleniti architecto modi natus,
							quos ducimus! Repudiandae reiciendis totam sequi veniam necessitatibus, magni harum. Lorem ipsum, dolor sit amet consectetur
							adipisicing elit. Culpa corrupti iusto dolor. Similique quibusdam eveniet quae deleniti architecto modi natus, quos ducimus!
							Repudiandae reiciendis totam sequi veniam necessitatibus, magni harum. Lorem ipsum, dolor sit amet consectetur adipisicing
							elit. Culpa corrupti iusto dolor. Similique quibusdam eveniet quae deleniti architecto modi natus, quos ducimus! Repudiandae
							reiciendis totam sequi veniam necessitatibus, magni harum. Lorem ipsum, dolor sit amet consectetur adipisicing elit. Culpa
							corrupti iusto dolor. Similique quibusdam eveniet quae deleniti architecto modi natus, quos ducimus! Repudiandae reiciendis
							totam sequi veniam necessitatibus, magni harum. Lorem ipsum, dolor sit amet consectetur adipisicing elit. Culpa corrupti iusto
							dolor. Similique quibusdam eveniet quae deleniti architecto modi natus, quos ducimus! Repudiandae reiciendis totam sequi
							veniam necessitatibus, magni harum. Lorem ipsum, dolor sit amet consectetur adipisicing elit. Culpa corrupti iusto dolor.
							Similique quibusdam eveniet quae deleniti architecto modi natus, quos ducimus! Repudiandae reiciendis totam sequi veniam
							necessitatibus, magni harum. Lorem ipsum, dolor sit amet consectetur adipisicing elit. Culpa corrupti iusto dolor. Similique
							quibusdam eveniet quae deleniti architecto modi natus, quos ducimus! Repudiandae reiciendis totam sequi veniam necessitatibus,
							magni harum. Lorem ipsum, dolor sit amet consectetur adipisicing elit. Culpa corrupti iusto dolor. Similique quibusdam eveniet
							quae deleniti architecto modi natus, quos ducimus! Repudiandae reiciendis totam sequi veniam necessitatibus, magni harum.
							Lorem ipsum, dolor sit amet consectetur adipisicing elit. Culpa corrupti iusto dolor. Similique quibusdam eveniet quae
							deleniti architecto modi natus, quos ducimus! Repudiandae reiciendis totam sequi veniam necessitatibus, magni harum.
						</p>
					</div>
				</svelte:fragment>
				<svelte:fragment slot="source">
					<CodeBlock
						language="html"
						code={`
<div class="card p-4 max-h-[200px] overflow-auto space-y-4">
	<h3 data-toc-ignore>Test Scrolling Here</h3>
	<p>
		Lorem ipsum, dolor sit...
	</p>
</div>			
			`}
					/>
				</svelte:fragment>
			</DocsPreview>
			<!--Dividers -->
			<div class="space-y-4">
				<h2>Dividers</h2>
				<p>
					Native <code>hr</code> horizontal rule elements respect your theme settings automatically. Use border size to adjust the width.
				</p>
				<DocsPreview background="neutral">
					<svelte:fragment slot="preview">
						<div class="w-full space-y-4">
							<hr />
							<hr class="!border-t-2" />
							<hr class="!border-t-4" />
							<hr class="!border-t-8" />
						</div>
					</svelte:fragment>
					<svelte:fragment slot="footer">
						<!-- prettier-ignore -->
						<div class="text-center">
						Use Tailwind's <a href="https://tailwindcss.com/docs/border-width" target="_blank" rel="noreferrer">Border Width Top</a> and <a href="https://tailwindcss.com/docs/divide-style" target="_blank" rel="noreferrer">Border Styles</a> to customize each divider.
					</div>
					</svelte:fragment>
					<svelte:fragment slot="source">
						<CodeBlock
							language="html"
							code={`
<hr />
<hr class="!border-t-2" />
<hr class="!border-t-4" />
<hr class="!border-t-8" />
					`}
						/>
					</svelte:fragment>
				</DocsPreview>
				<h3>Divider Styling</h3>
				<p>Dividers may be dashed, dotted, or doubled.</p>
				<DocsPreview background="neutral">
					<svelte:fragment slot="preview">
						<div class="w-full space-y-4">
							<hr class="!border-dashed" />
							<hr class="!border-dotted" />
							<hr class="!border-t-8 !border-double" />
						</div>
					</svelte:fragment>
					<svelte:fragment slot="source">
						<CodeBlock
							language="html"
							code={`
<hr class="!border-dashed" />
<hr class="!border-dotted" />
<hr class="!border-t-8 !border-double" />
					`}
						/>
					</svelte:fragment>
				</DocsPreview>
				<h3>Vertical Dividers</h3>
				<p>
					Divide columns with the <code>.divider-vertical</code> class. You can apply it with a <code>span</code> tag. Adjust the
					<a href="https://tailwindcss.com/docs/height" target="_blank" rel="noreferrer">height</a> as desired.
				</p>
				<DocsPreview background="neutral">
					<svelte:fragment slot="preview">
						<div class="w-full grid grid-cols-3 gap-4 place-items-center">
							<p>Left</p>
							<span class="divider-vertical h-20" />
							<p>Right</p>
						</div>
					</svelte:fragment>
					<svelte:fragment slot="source">
						<CodeBlock language="html" code={`<span class="divider-vertical h-20" />`} />
					</svelte:fragment>
				</DocsPreview>
			</div>
		</div></svelte:fragment
	>
</DocsShell>
