<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import { Editor } from '@tiptap/core';
	import StarterKit from '@tiptap/starter-kit';

	let editor;
	let element;
	export let content: string | object;

	onMount(async () => {
		console.time('createDisplayEditor');
		editor = new Editor({
			element,
			extensions: [StarterKit],
			content: '',
			editable: false
		});

		try {
			editor.commands.setContent(content);
		} catch (error) {
			alert(error.message);
		}
		console.timeEnd('createDisplayEditor');
	});

	onDestroy(() => {
		if (editor) {
			editor.destroy();
		}
	});
</script>

<div class="border-red-200" bind:this={element}></div>
