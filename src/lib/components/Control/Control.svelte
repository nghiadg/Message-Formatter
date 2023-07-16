<script lang="ts">
	export let content: string = '';
	export let convertedContent: string = '';

	function convertUrls() {
		const regex = new RegExp(
			/(http|ftp|https):\/\/([\w_-]+(?:(?:\.[\w_-]+)+))([\w.,@?^=%&:\/~+#-]*[\w@?^=%&\/~+#-])/gm
		);
		const urls = content.match(regex);
		convertedContent = (urls || []).join('\n');
	}

</script>

<div class="d-flex flex-column flex-shrink-0 gap-3 justify-content-center controls">
	<button class="btn btn-outline-light btn-sm" on:click={convertUrls}>Convert URLs</button>
</div>

<style>
    .controls {
        width: 14rem;
    }
</style>