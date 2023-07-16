<script lang="ts">
	import Control from "$lib/components/Control/Control.svelte";
    import TextEditor from "$lib/components/TextEditor/TextEditor.svelte";
    let content: string = '';
    let convertedContent: string = '';
</script>

<div class="container vh-100">
    <div class="d-flex gap-3 align-items-center justify-content-center h-100">
        <TextEditor title="Message" bind:content={content} />
        <Control content={content} bind:convertedContent={convertedContent}/>
        <TextEditor title="URLs Converted" bind:content={convertedContent} hasBtnOpenUrls={true}/>
    </div>
</div>