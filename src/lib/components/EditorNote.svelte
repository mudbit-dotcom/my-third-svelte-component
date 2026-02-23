<!--
@component
EditorNote.svelte — Editor's Note Box

A styled box component for editor's notes within articles.
Features a distinctive border and background to separate editorial content.

USAGE EXAMPLE:
<EditorNote>
  <p>This article was updated November 13th, 2025 to include new information.</p>
</EditorNote>
-->
<script>
  let {
    children,         // The editor's note content
  } = $props();
</script>

<aside class="editor-note">
  <div class="editor-note__label">Editor's Note</div>
  <div class="editor-note__content">
    {@render children()}
  </div>
</aside>

<style lang="scss">
  @use '../styles' as *;

  .editor-note {
    background-color: var(--color-light-gray);
    border-left: var(--border-width-accent) solid var(--color-cuny-blue);
    padding: var(--spacing-md);
    margin: var(--spacing-lg) 0;
    border-radius: 4px;
  }

  .editor-note__label {
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    color: var(--color-cuny-blue);
    margin-bottom: var(--spacing-xs);
  }

  .editor-note__content {
    font-family: var(--font-sans);
    font-size: var(--font-size-base);
    line-height: 1.6;
    color: var(--color-text);
  }

  /* Paragraph styling within editor's note */
  .editor-note__content :global(p) {
    margin-bottom: var(--spacing-sm);
  }

  .editor-note__content :global(p:last-child) {
    margin-bottom: 0;
  }

  /* Links within editor's note */
  .editor-note__content :global(a) {
    color: var(--color-cuny-blue);
    text-decoration: underline;
    text-underline-offset: 2px;
  }

  .editor-note__content :global(a:hover) {
    color: var(--color-accent-hover);
  }

  /* Responsive: larger padding on desktop */
  @include desktop {
    .editor-note {
      padding: var(--spacing-lg);
    }
  }
</style>
