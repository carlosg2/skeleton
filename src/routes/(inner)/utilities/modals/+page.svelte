<script lang="ts">
	// Docs
	import DocsShell from '$docs/layouts/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings } from '$docs/layouts/DocsShell/types';
	import DocsPreview from '$docs/components/DocsPreview/DocsPreview.svelte';
	// Modal Examples (see also root layout)
	import ModalExampleForm from '$docs/modals/examples/ModalExampleForm.svelte';
	// Components
	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';
	import Accordion from '$lib/components/Accordion/Accordion.svelte';
	import AccordionItem from '$lib/components/Accordion/AccordionItem.svelte';
	import TabGroup from '$lib/components/Tab/TabGroup.svelte';
	import Tab from '$lib/components/Tab/Tab.svelte';

	// Sveld
	import sveldModal from '$lib/utilities/Modal/Modal.svelte?raw&sveld';

	// Modals Utils
	import type { ModalSettings, ModalComponent } from '$lib/utilities/Modal/types';
	import { modalStore } from '$lib/utilities/Modal/stores';

	// Stores
	let tabCustom: string = 'register';

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Utility,
		name: 'Modals',
		description: 'High priority dialogs and modals using a dynamic queue system.',
		imports: ['Modal', 'modalStore'],
		types: ['ModalSettings', 'ModalComponent'],
		source: 'utilities/Modal',
		aria: 'https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/',
		components: [{ sveld: sveldModal }],
		keyboard: [['<kbd>Esc</kbd>', ' Dismisses the foremost modal.']],
		classes: [
			['<code>.w-modal</code>', '-', 'Sets a standard responsive width for modals.'],
			['<code>.w-modal-slim</code>', '-', 'Create a slimmer modal. Great for small component modals.'],
			['<code>.w-modal-wide</code>', '-', 'Create a wider modal. Great for full screen component modals.']
		]
	};

	// Demo ---

	function modalDemo(): void {
		const d: ModalSettings = {
			type: 'alert',
			title: 'Hello Skeleton',
			body: 'This modal example includes a title, body, and image.',
			image: 'https://i.imgur.com/TykCy5e.gif'
			// image: 'https://i.imgur.com/WOgTG96.gif'
		};
		modalStore.trigger(d);
	}

	// Variants ---

	function modalAlert(): void {
		const d: ModalSettings = {
			type: 'alert',
			title: 'Hello World!',
			body: 'This simple alert modal uses <code>type: alert</code>.'
		};
		modalStore.trigger(d);
	}

	function modalConfirm(): void {
		const d: ModalSettings = {
			type: 'confirm',
			title: 'Please Confirm',
			body: 'Are you sure you wish to proceed?',
			response: (r: boolean) => {
				if (r) console.log('response:', r);
			}
		};
		modalStore.trigger(d);
	}

	function modalPrompt(): void {
		const d: ModalSettings = {
			type: 'prompt',
			title: 'Enter Name',
			body: 'Provide your first name in the field below.',
			value: 'Skeleton',
			valueAttr: { type: 'text', minlength: 3, maxlength: 10, required: true },
			response: (r: string) => {
				if (r) console.log('response:', r);
			}
		};
		modalStore.trigger(d);
	}

	function modalMultiple(): void {
		[1, 2, 3].forEach((dNum: number) => {
			const d: ModalSettings = {
				type: 'alert',
				title: `Modal ${dNum}`,
				body: `The modal body of ${dNum}.`
			};
			modalStore.trigger(d);
		});
	}

	// Custom ---

	function modalComponentForm(): void {
		const c: ModalComponent = { ref: ModalExampleForm };
		const d: ModalSettings = {
			type: 'component',
			component: c,
			title: 'Custom Form Component',
			body: 'Complete the form below and then press submit.',
			response: (r: any) => {
				if (r) console.log('response:', r);
			}
		};
		modalStore.trigger(d);
	}

	function modalComponentList(): void {
		const d: ModalSettings = {
			type: 'component',
			component: 'exampleList',
			title: 'Custom List Component',
			body: 'Make your selection then press submit.',
			response: (r: any) => {
				if (r) console.log('response:', r);
			}
		};
		modalStore.trigger(d);
	}

	function modalComponentEmbed(): void {
		const d: ModalSettings = {
			type: 'component',
			component: 'exampleEmbed'
		};
		modalStore.trigger(d);
	}

	function modalComponentImage(): void {
		const d: ModalSettings = {
			type: 'component',
			component: 'exampleImage',
			image: 'https://i.imgur.com/WOgTG96.gif',
			meta: { source: 'Silly Symphonies - The Skeleton Dance' }
		};
		modalStore.trigger(d);
	}
</script>

<DocsShell {settings}>
	<!-- Slot: Sandbox -->
	<svelte:fragment slot="sandbox">
		<DocsPreview>
			<svelte:fragment slot="preview">
				<button class="btn variant-filled" on:click={modalDemo}>Show Modal</button>
			</svelte:fragment>
			<svelte:fragment slot="source">
				<p>Implement a single instance of the modal component in your app's root layout above the App Shell (if present).</p>
				<CodeBlock language="html" code={`<Modal />\n\n<!-- <AppShell>...</AppShell> -->`} />
			</svelte:fragment>
		</DocsPreview>
	</svelte:fragment>

	<!-- /actions/focus-trap -->

	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<!-- prettier-ignore -->
		<aside class="alert alert-message variant-ghost-warning">
			<p>
				This feature uses the <a href="https://en.wikipedia.org/wiki/Singleton_pattern" target="_blank" rel="noreferrer">Singleton pattern</a>, meaning you should aim to implement a <u>single instance of the component per project</u>, but it will remain globally scoped
				and reusable via a Svelte writable store. Do not reimplement this component for each route page.
			</p>
		</aside>
		<section class="space-y-4">
			<h2>Modal Store</h2>
			<p>When you wish to trigger a modal, import the <code>modalStore</code>, which acts as the modal queue.</p>
			<CodeBlock language="ts" code={`import { modalStore } from '@skeletonlabs/skeleton';`} />
			<h3>Trigger</h3>
			<p>The <code>title</code>, <code>body</code>, and <code>image</code> are available to all modals.</p>
			<!-- Alert -->
			<DocsPreview background="neutral">
				<svelte:fragment slot="preview">
					<div class="flex gap-4">
						<button class="btn variant-filled" on:click={modalAlert}>Alert Modal</button>
						<button class="btn variant-filled" on:click={modalMultiple}>Queue Multiple</button>
					</div>
				</svelte:fragment>
				<svelte:fragment slot="source">
					<CodeBlock
						language="ts"
						code={`
const alert: ModalSettings = {
	type: 'alert',
	// Data
	title: 'Example Alert',
	body: 'This is an example modal.',
	image: 'https://i.imgur.com/WOgTG96.gif',
};
modalStore.trigger(alert);
`}
					/>
				</svelte:fragment>
			</DocsPreview>
			<!-- Confirm -->
			<DocsPreview background="neutral">
				<svelte:fragment slot="preview">
					<button class="btn variant-filled" on:click={modalConfirm}>Confirm Modal</button>
				</svelte:fragment>
				<svelte:fragment slot="source">
					<CodeBlock
						language="ts"
						code={`
const confirm: ModalSettings = {
	type: 'confirm',
	// Data
	title: 'Please Confirm',
	body: 'Are you sure you wish to proceed?',
	// TRUE if confirm pressed, FALSE if cancel pressed
	response: (r: boolean) => console.log('response:', r),
};
modalStore.trigger(confirm);
`}
					/>
				</svelte:fragment>
			</DocsPreview>
			<!-- Prompt -->
			<DocsPreview background="neutral">
				<svelte:fragment slot="preview">
					<button class="btn variant-filled" on:click={modalPrompt}>Prompt Modal</button>
				</svelte:fragment>
				<svelte:fragment slot="source">
					<CodeBlock
						language="ts"
						code={`
const prompt: ModalSettings = {
	type: 'prompt',
	// Data
	title: 'Enter Name',
	body: 'Provide your first name in the field below.',
	// Populates the input value and attributes
	value: 'Skeleton',
	valueAttr: { type: 'text', minlength: 3, maxlength: 10, required: true },
	// Returns the updated response value
	response: (r: string) => console.log('response:', r),
};
modalStore.trigger(prompt);
`}
					/>
				</svelte:fragment>
			</DocsPreview>
			<!-- Close -->
			<h3>Close</h3>
			<p>Trigger the <code>close()</code> method to remove the first modal in the modal queue.</p>
			<CodeBlock language="ts" code={`modalStore.close();`} />
			<!-- Clear -->
			<h3>Clear</h3>
			<p>Trigger the <code>clear()</code> method to completely empty the modal queue.</p>
			<CodeBlock language="ts" code={`modalStore.clear();`} />
		</section>
		<!-- Modal Settings -->
		<section class="space-y-4">
			<h2>Modal Settings</h2>
			<p>These additional settings are available to all modals.</p>
			<!-- prettier-ignore -->
			<CodeBlock
				language="ts"
				code={`
const d: ModalSettings = {\n
	// Provide arbitrary classes to the backdrop and modal elements:
	backdropClasses: '!bg-green-500',
	modalClasses: '!bg-red-500',\n
	// Provide arbitrary metadata to your modal instance:
	meta: { foo: 'bar', fizz: 'buzz', fn: myCustomFunction }\n
};`}
			/>
		</section>
		<!-- Component Modals -->
		<section class="space-y-4">
			<div class="flex items-center space-x-2">
				<h2>Component Modals</h2>
				<span class="badge variant-filled-warning">Advanced</span>
			</div>
			<p>To create custom modals, generate a new component, then pass this to the Modal system.</p>
			<DocsPreview background="neutral">
				<svelte:fragment slot="preview">
					<div class="grid grid-cols-1 md:grid-cols-4 gap-4 md:max-w-[480px] mx-auto">
						<button class="btn variant-filled" on:click={modalComponentForm}>Form</button>
						<button class="btn variant-filled" on:click={modalComponentList}>List</button>
						<button class="btn variant-filled" on:click={modalComponentEmbed}>Embed</button>
						<button class="btn variant-filled" on:click={modalComponentImage}>Image</button>
					</div>
				</svelte:fragment>
				<svelte:fragment slot="footer">
					<div class="text-center">
						<!-- prettier-ignore -->
						<a class="btn variant-ghost" href="https://github.com/skeletonlabs/skeleton/tree/master/src/docs/modals/examples" target="_blank" rel="noreferrer">View Source Code</a>
					</div>
				</svelte:fragment>
				<svelte:fragment slot="source">
					<TabGroup regionPanel="space-y-4">
						<Tab bind:group={tabCustom} name="component-modals" value="register">Reuasble Registry</Tab>
						<Tab bind:group={tabCustom} name="component-modals" value="direct">Direct Method</Tab>
						<!-- Panel -->
						<svelte:fragment slot="panel">
							{#if tabCustom === 'register'}
								<!-- prettier-ignore -->
								<p>
									Import custom components in your root layout, create a modal registry object, then pass this object to the Modal <code>components</code> property.
								</p>
								<CodeBlock
									language="ts"
									code={`
// import ModalComponentOne from '...';
// import ModalComponentTwo from '...';\n
const modalComponentRegistry: Record<string, ModalComponent> = {\n
	// Custom Modal 1
	modalComponentOne: {
		// Pass a reference to your custom component
		ref: ModalComponentOne,
		// Add the component properties as key/value pairs
		props: { background: 'bg-red-500' },
		// Provide a template literal for the default component slot
		slot: '<p>Skeleton</p>'
	},\n
	// Custom Modal 2
	modalComponentTwo: { ref: ModalComponentTwo },\n
	// ...
};
									`}
								/>
								<CodeBlock language="html" code={`<Modal components={modalComponentRegistry} />`} />
								<p>When triggering a component, pass <code>component: string</code>, where the value represents the registry object key.</p>
								<CodeBlock
									language="ts"
									code={`
const d: ModalSettings = {
	type: 'component',
	// Pass the component registry key as a string:
	component: 'modalComponentOne',
};
modalStore.trigger(d);
									`}
								/>
							{:else if tabCustom === 'direct'}
								<p>
									For one-off components you can create a <code>ModalComponent</code> object containing your component, props, and slot values.
								</p>
								<CodeBlock
									language="ts"
									code={`
// import MyCustomComponent from '...';\n
const modalComponent: ModalComponent = {
	// Pass a reference to your custom component
	ref: MyCustomComponent,
	// Add the component properties as key/value pairs
	props: { background: 'bg-red-500' },
	// Provide a template literal for the default component slot
	slot: '<p>Skeleton</p>'
};
									`}
								/>
								<p>
									When triggering a component, pass the <code>component: ModalComponent</code> directly to <code>ModalSettings</code>.
								</p>
								<CodeBlock
									language="ts"
									code={`
const d: ModalSettings = {
	type: 'component',
	// Pass the component directly:
	component: modalComponent,
};
modalStore.trigger(d);
									`}
								/>
							{/if}
						</svelte:fragment>
					</TabGroup>
				</svelte:fragment>
			</DocsPreview>
			<p>See the additional information below to learn how to use custom component modals.</p>
			<Accordion autocollapse class="card variant-glass p-4">
				<AccordionItem open>
					<svelte:fragment slot="summary"><h3 data-toc-ignore>Accessing Store Data</h3></svelte:fragment>
					<svelte:fragment slot="content">
						<p>
							Import and use the <code>modalStore</code>. All provide data is available within your component via
							<code>$modalStore[0]</code>.
						</p>
					</svelte:fragment>
				</AccordionItem>
				<AccordionItem>
					<svelte:fragment slot="summary"><h3 data-toc-ignore>The Visible Modal</h3></svelte:fragment>
					<svelte:fragment slot="content">
						<p>The foremost and visible modal in your queue uses index zero <code>$modalStore[0]</code>.</p>
					</svelte:fragment>
				</AccordionItem>
				<AccordionItem>
					<svelte:fragment slot="summary"><h3 data-toc-ignore>Modal Parent Properties</h3></svelte:fragment>
					<svelte:fragment slot="content">
						<p>
							The Modal component in your root layout is considered the "parent" component. Your custom modal component will be generated
							within this. All properties for the parent component are passed down via the <code>parent</code> prop. For example
							<code>parent.background</code> would provide the <em>background</em> property value.
						</p>
						<p>Tap the <em>Props</em> tab on this page to view a full list of available <code>parent</code> props.</p>
					</svelte:fragment>
				</AccordionItem>
				<AccordionItem>
					<svelte:fragment slot="summary"><h3 data-toc-ignore>Triggering a Response</h3></svelte:fragment>
					<svelte:fragment slot="content">
						<p>
							Use the <code>$modalStore[0].response('myResponseDataHere');</code> trigger the response function and return a value.
						</p>
					</svelte:fragment>
				</AccordionItem>
				<AccordionItem>
					<svelte:fragment slot="summary"><h3 data-toc-ignore>Closing a Modal</h3></svelte:fragment>
					<svelte:fragment slot="content">
						<p>Use the <code>parent.onClose()</code> or <code>modalStore.close()</code> methods to close the modal.</p>
					</svelte:fragment>
				</AccordionItem>
				<AccordionItem>
					<svelte:fragment slot="summary"><h3 data-toc-ignore>Accessing Metadata</h3></svelte:fragment>
					<svelte:fragment slot="content">
						<p>Arbitrary metadata is available using <code>$modalStore[0].meta?.someKey</code>.</p>
					</svelte:fragment>
				</AccordionItem>
				<AccordionItem>
					<svelte:fragment slot="summary"><h3 data-toc-ignore>Standarize Modal Widths</h3></svelte:fragment>
					<svelte:fragment slot="content">
						<p>
							View the <em>Classes</em> tab at the top of this page to view optional modal helper classes. These included
							<code>.w-modal</code>,
							<code>.w-modal-slim</code>, and <code>.w-modal-wide</code>, which represent standard, slim, and wide presets.
						</p>
					</svelte:fragment>
				</AccordionItem>
			</Accordion>
		</section>
		<section class="space-y-4">
			<h2>Accessibility</h2>
			<!-- prettier-ignore -->
			<p>Skeleton <u>does not</u> provide a means to disable the backdrop's click to close feature, as this would be harmful to accessibility. View the <a href="https://www.w3.org/WAI/ARIA/apg/patterns/dialogmodal/" target="_blank" rel="noreferrer">ARIA APG guidelines</a> to learn more about modal accessibility.</p>
		</section>
		<!-- SvelteKit SSR Warning -->
		<!-- prettier-ignore -->
		<section class="space-y-4">
			<h2>SvelteKit SSR Warning</h2>
			<div class="space-y-4">
				<div class="!flex flex-col md:flex-row justify-between items-center space-y-4 md:space-y-0 md:space-x-4">
					<p>There are known security risks when using Svelte writable stores within SvelteKit load functions.</p>
					<a class="btn variant-filled" href="https://github.com/skeletonlabs/skeleton/wiki/SvelteKit-SSR-Warning" target="_blank" rel="noreferrer">Details &rarr;</a>
				</div>
			</div>
		</section>
	</svelte:fragment>
</DocsShell>
