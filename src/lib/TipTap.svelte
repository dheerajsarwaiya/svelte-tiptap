<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import { Editor } from '@tiptap/core';
	import StarterKit from '@tiptap/starter-kit';

	let editorEditable;
	let editorView;
	let elementEditable;
	let elementView;

	onMount(async () => {
		editorEditable = new Editor({
			element: elementEditable,
			extensions: [StarterKit],
			content: ''
		});

		editorView = new Editor({
			element: elementView,
			extensions: [StarterKit],
			content: '',
			editable: false // disable editing
		});

		// Update the content of the read-only editor when the content of the editable editor changes
		editorEditable.on('update', () => {
			const content = editorEditable.getJSON();
			editorView.commands.setContent(content);
		});
	});

	onDestroy(() => {
		if (editorEditable) {
			editorEditable.destroy();
		}
		if (editorView) {
			editorView.destroy();
		}
	});
</script>

<div class="editor-container">
	<div class="editor" bind:this={elementEditable}></div>
	<div class="editor" bind:this={elementView}></div>
</div>

<style>
	.editor-container {
		display: flex;
		flex-direction: column;
		height: 100vh;
	}

	.editor {
		flex: 1;
		overflow: auto;
		border: 1px solid #ccc;
		margin-bottom: 1rem;
	}
</style>
