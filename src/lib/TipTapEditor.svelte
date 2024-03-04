<script lang="ts">
	import StarterKit from '@tiptap/starter-kit';
	import { Editor } from '@tiptap/core';
	import { onMount } from 'svelte';
	import Toolbar from './Toolbar.svelte';
	import Table from '@tiptap/extension-table';
	import TableCell from '@tiptap/extension-table-cell';
	import TableHeader from '@tiptap/extension-table-header';
	import TableRow from '@tiptap/extension-table-row';
	import './styles.scss';

	let element;
	let editor: Editor | null;
	export let editable = false;

	onMount(() => {
		console.time('create editor');
		editor = new Editor({
			element: element,
			extensions: [
				StarterKit,
				Table.configure({
					resizable: true
				}),
				TableRow,
				TableHeader,
				TableCell
			],
			editable: editable,
			editorProps: {
				attributes: {
					class: 'p-4 border-2 border-gray-300 rounded-md'
				}
			},
			content: `
              <h2>
                Hi there,
              </h2>
              <p>
                this is a <em>basic</em> example of <strong>tiptap</strong>. Sure, there are all kind of basic text styles you’d probably expect from a text editor. But wait until you see the lists:
              </p>
              <ul>
                <li>
                  That’s a bullet list with one …
                </li>
                <li>
                  … or two list items.
                </li>
              </ul>
              <p>
                Isn’t that great? And all of that is editable. But wait, there’s more. Let’s try a code block:
              </p>
              <pre><code class="language-css">body {
          display: none;
        }</code></pre>
              <p>
                I know, I know, this is impressive. It’s only the tip of the iceberg though. Give it a try and click a little bit around. Don’t forget to check the other examples too.
              </p>
              <blockquote>
                Wow, that’s amazing. Good work, boy! 👏
                <br />
                — Mom
              </blockquote>
            `,
			onTransaction: () => {
				// force re-render so `editor.isActive` works as expected
				editor = editor;
			}
		});
		console.timeEnd('create editor');
	});
</script>

{#if editor && editable}
	<Toolbar {editor} />
{/if}
<div class="element m-4 mt-0" bind:this={element} />
