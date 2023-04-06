<template>
    <div>
      <editor-content :editor="editor" />
  
      <div class="character-count" v-if="editor">
        {{ editor.storage.characterCount.characters() }}/{{ limit }} characters
        <br>
        {{ editor.storage.characterCount.words() }} words
      </div>
    </div>
  </template>
  
  <script>
  import CharacterCount from '@tiptap/extension-character-count'
  import Document from '@tiptap/extension-document'
  import Paragraph from '@tiptap/extension-paragraph'
  import Text from '@tiptap/extension-text'
  import { Editor, EditorContent } from '@tiptap/vue-2'
  
  export default {
    components: {
      EditorContent,
    },
    data() {
      return {
        editor: null,
        limit: 280,
      }
    },
    mounted() {
      this.editor = new Editor({
        extensions: [
          Document,
          Paragraph,
          Text,
          CharacterCount,
        ],
        content: null,
        onUpdate: () => {
            console.log('Update Called')
        }
      })
    },
  
    beforeUnmount() {
      this.editor.destroy()
    },
  }
  </script>
  
  <style lang="scss">
  /* Basic editor styles */
  .ProseMirror {
    > * + * {
      margin-top: 0.75em;
    }
    height: 300px;
    width: 500px;
  }
  
  .character-count {
    margin-top: 1rem;
    color: #868e96;
  }
  </style>