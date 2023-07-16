<script lang="ts">
	import IconCheck from '$lib/icons/IconCheck/IconCheck.svelte';
	import IconCopy from '$lib/icons/IconCopy/IconCopy.svelte';
	import IconLink from '$lib/icons/IconLink/IconLink.svelte';
	const TIMEOUT_SHOW_COPIED = 1000;

	export let title: string = '';
	export let content: string = '';
	export let hasBtnOpenUrls: boolean = false;

	let editor: HTMLDivElement;
	let isCopied: boolean = false;

	function changeTextContent(e: Event) {
		const target = e.target as HTMLDivElement;
		content = target.textContent?.trim() || '';
	}

	function copyTextContent() {
		navigator.clipboard.writeText(content);
		isCopied = true;
		setTimeout(() => {
			isCopied = false;
		}, TIMEOUT_SHOW_COPIED);
	}

	function openUrls() {
		const urls = content.split('\n');
		urls.forEach((url) => {
			window.open(url, '_blank');
		});
	}
</script>

<div class="w-100 editor d-flex flex-column bg-white">
	<div
		class="px-2 py-1 border-bottom bg-darksea text-editor fs-small d-flex align-items-center justify-content-between"
	>
		<span>{title}</span>
		<div class="d-flex gap-3 align-items-center justify-content-center">
			{#if hasBtnOpenUrls}
				<div
					role="button"
					class="btn-copy"
					title="Open URLs"
					on:click={openUrls}
					aria-hidden="true"
				>
					<IconLink />
				</div>
			{/if}
			<div
				role="button"
				class="btn-copy"
				title="Copy Message"
				on:click={copyTextContent}
				aria-hidden="true"
			>
				{#if isCopied}
					<IconCheck />
				{:else}
					<IconCopy />
				{/if}
			</div>
		</div>
	</div>
	<div class="p-2 flex-fill">
		<div
			bind:this={editor}
			contenteditable="true"
			on:input={changeTextContent}
			bind:textContent={content}
			class="h-100 fs-small editor__input"
		/>
	</div>
</div>

<style>
	.editor {
		height: 88vh;
	}

	.editor__input {
		outline: none;
		white-space: pre-wrap;
	}

	.btn-copy {
		cursor: pointer;
	}
	.btn-copy:hover {
		color: var(--bs-active);
	}
</style>
