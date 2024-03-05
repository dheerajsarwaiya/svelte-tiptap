<script lang="ts">
	export let editor;
	import { Button } from '$lib/components/ui/button';
	import {
		Bold,
		Heading1,
		Heading2,
		Heading3,
		Italic,
		List,
		ListOrdered,
		Minus,
		Code,
		Quote,
		Undo,
		Redo,
		Table,
		BetweenVerticalStart,
		BetweenHorizontalStart
	} from 'lucide-svelte';

	function addImageUrl() {
		const url = prompt('Enter the URL of the image:');
		if (url) {
			editor.commands.setImage({ src: url });
		}
	}
</script>

<div class="m-4 my-1 border border-input bg-transparent rounded-md">
	<Button
		variant={editor.isActive('bold') ? 'default' : 'ghost'}
		on:click={() => console.log && editor.chain().focus().toggleBold().run()}
		disabled={!editor.can().chain().focus().toggleBold().run()}
		size="sm"
	>
		<Bold class="h-4 w-4" />
	</Button>
	<Button
		variant={editor.isActive('italic') ? 'default' : 'ghost'}
		on:click={() => editor.chain().focus().toggleItalic().run()}
		disabled={!editor.can().chain().focus().toggleItalic().run()}
		size="sm"
	>
		<Italic class="h-4 w-4" />
	</Button>
	<!-- <Button
		variant="ghost"
		on:click={() => editor.chain().focus().toggleStrike().run()}
		disabled={!editor.can().chain().focus().toggleStrike().run()}
		class={editor.isActive('strike') ? 'is-active' : ''}
		size="sm"
	>
		<Strikethrough class="h-4 w-4" />
	</Button> -->

	<Button
		variant={editor.isActive('heading', { level: 1 }) ? 'default' : 'ghost'}
		on:click={() => editor.chain().focus().toggleHeading({ level: 1 }).run()}
		size="sm"
	>
		<Heading1 class="h-4 w-4" />
	</Button>
	<Button
		variant={editor.isActive('heading', { level: 2 }) ? 'default' : 'ghost'}
		on:click={() => editor.chain().focus().toggleHeading({ level: 2 }).run()}
		class={editor.isActive('heading', { level: 2 }) ? 'is-active' : ''}
		size="sm"
	>
		<Heading2 class="h-4 w-4" />
	</Button>
	<Button
		variant={editor.isActive('heading', { level: 3 }) ? 'default' : 'ghost'}
		on:click={() => editor.chain().focus().toggleHeading({ level: 3 }).run()}
		class={editor.isActive('heading', { level: 3 }) ? 'is-active' : ''}
		size="sm"
	>
		<Heading3 class="h-4 w-4" />
	</Button>
	<!-- <Button variant="ghost" 
		on:click={() => editor.chain().focus().toggleHeading({ level: 4 }).run()}
		class={editor.isActive('heading', { level: 4 }) ? 'is-active' : ''}
	>
		<Heading4 />
	</Button> -->

	<Button
		variant={editor.isActive('bulletList') ? 'default' : 'ghost'}
		on:click={() => editor.chain().focus().toggleBulletList().run()}
		size="sm"
	>
		<List class="h-4 w-4" />
	</Button>
	<Button
		variant={editor.isActive('orderedList') ? 'default' : 'ghost'}
		on:click={() => editor.chain().focus().toggleOrderedList().run()}
		size="sm"
	>
		<ListOrdered class="h-4 w-4" />
	</Button>
	<Button
		variant={editor.isActive('codeBlock') ? 'default' : 'ghost'}
		on:click={() => editor.chain().focus().toggleCodeBlock().run()}
		size="sm"
	>
		<Code class="h-4 w-4" />
	</Button>
	<Button
		variant={editor.isActive('blockquote') ? 'default' : 'ghost'}
		on:click={() => editor.chain().focus().toggleBlockquote().run()}
		size="sm"
	>
		<Quote class="h-4 w-4" />
	</Button>
	<Button variant="ghost" on:click={addImageUrl(editor)} size="sm">Image</Button>
	<Button
		variant="ghost"
		on:click={() => editor.chain().focus().setHorizontalRule().run()}
		size="sm"><Minus class="h-4 w-4" /></Button
	>
	<Button
		variant={editor.isActive('table') ? 'default' : 'ghost'}
		on:click={() => editor.commands.insertTable({ rows: 2, cols: 2, withHeaderRow: true })}
		size="sm"
	>
		<Table />
	</Button>
	{#if editor.isActive('table')}
		<Button variant="ghost" on:click={() => editor.commands.addColumnAfter()} size="sm">
			<BetweenVerticalStart />
		</Button>
		<Button variant="ghost" on:click={() => editor.commands.addRowAfter()} size="sm">
			<BetweenHorizontalStart />
		</Button>
	{/if}
	<Button
		variant="ghost"
		on:click={() => editor.chain().focus().undo().run()}
		disabled={!editor.can().chain().focus().undo().run()}
		size="sm"
	>
		<Undo class="h-4 w-4" />
	</Button>
	<Button
		variant="ghost"
		on:click={() => editor.chain().focus().redo().run()}
		disabled={!editor.can().chain().focus().redo().run()}
		size="sm"
	>
		<Redo class="h-4 w-4" />
	</Button>
</div>
