<template>
  <div>
    <h1 class="text-center font-bold text-2xl">Text Editor!</h1>
    <div v-if="editor">
      <button
        @click="editor.chain().focus().toggleBold().run()"
        :disabled="!editor.can().chain().focus().toggleBold().run()"
        :class="[
          'px-3 py-1 border rounded hover:bg-blue-200 transition my-3',
          editor.isActive('bold')
            ? 'border-blue-600 text-blue-500 font-bold'
            : 'border-gray-300 ',
        ]"
      >
        B
      </button>
      <button
        @click="editor.chain().focus().toggleItalic().run()"
        :disabled="!editor.can().chain().focus().toggleItalic().run()"
        :class="[
          'px-3 py-1 border rounded hover:bg-blue-200 transition my-3 ml-4',
          editor.isActive('italic')
            ? 'border-blue-600 text-blue-500 font-bold'
            : 'border-gray-300 ',
        ]"
      >
        I
      </button>
    </div>
    <TiptapEditorContent
      :editor="editor"
      class="border border-gray-300 rounded-lg min-h-[100px] p-2"
    />
  </div>
</template>

<script setup>
import Placeholder from "@tiptap/extension-placeholder";
const editor = useEditor({
  content: "<p> <br/>  <br/> <br/> <br/> <br/></p>",
  extensions: [
    TiptapStarterKit,
    Placeholder.configure({
      placeholder: "Type something here...",
    }),
  ],
});

onBeforeUnmount(() => {
  unref(editor).destroy();
});
</script>
