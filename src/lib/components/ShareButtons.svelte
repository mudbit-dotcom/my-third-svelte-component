<!--
@component
ShareButtons.svelte — Social Media Share Buttons

A group of share buttons for LinkedIn, Instagram, and Facebook.
Provides easy social sharing functionality for articles.

USAGE EXAMPLE:
<ShareButtons 
  url="https://example.com/article" 
  title="Article Title"
/>
-->
<script>
  let {
    url = '',              // URL to share (defaults to current page)
    title = '',            // Title/text to share
  } = $props();

  // Use current page URL if not provided
  const shareUrl = url || (typeof window !== 'undefined' ? window.location.href : '');
  const shareTitle = encodeURIComponent(title);
  const encodedUrl = encodeURIComponent(shareUrl);

  // Social media share URLs
  const linkedInUrl = `https://www.linkedin.com/sharing/share-offsite/?url=${encodedUrl}`;
  const facebookUrl = `https://www.facebook.com/sharer/sharer.php?u=${encodedUrl}`;
  // Note: Instagram doesn't support direct web sharing, so this opens Instagram
  const instagramUrl = `https://www.instagram.com/`;

  function handleShare(platform) {
    if (platform === 'instagram') {
      // Instagram doesn't have web sharing - could show a message or open app
      window.open(instagramUrl, '_blank', 'noopener,noreferrer');
    } else {
      // Open share window for other platforms
      const width = 600;
      const height = 400;
      const left = (window.screen.width - width) / 2;
      const top = (window.screen.height - height) / 2;
      const features = `width=${width},height=${height},left=${left},top=${top}`;
      
      if (platform === 'linkedin') {
        window.open(linkedInUrl, '_blank', features);
      } else if (platform === 'facebook') {
        window.open(facebookUrl, '_blank', features);
      }
    }
  }
</script>

<div class="share-buttons">
  <span class="share-buttons__label">Share:</span>
  <div class="share-buttons__group">
    <button 
      class="share-button share-button--linkedin" 
      onclick={() => handleShare('linkedin')}
      aria-label="Share on LinkedIn"
    >
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
        <path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/>
      </svg>
      <span class="share-button__text">LinkedIn</span>
    </button>
    
    <button 
      class="share-button share-button--facebook" 
      onclick={() => handleShare('facebook')}
      aria-label="Share on Facebook"
    >
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
        <path d="M9 8h-3v4h3v12h5v-12h3.642l.358-4h-4v-1.667c0-.955.192-1.333 1.115-1.333h2.885v-5h-3.808c-3.596 0-5.192 1.583-5.192 4.615v3.385z"/>
      </svg>
      <span class="share-button__text">Facebook</span>
    </button>
    
    <button 
      class="share-button share-button--instagram" 
      onclick={() => handleShare('instagram')}
      aria-label="Share on Instagram"
    >
      <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
        <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
      </svg>
      <span class="share-button__text">Instagram</span>
    </button>
  </div>
</div>

<style lang="scss">
  @use '../styles' as *;

  .share-buttons {
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
    margin: var(--spacing-lg) 0;
    padding: var(--spacing-md) 0;
    border-top: var(--border-width-thin) solid var(--color-border);
    border-bottom: var(--border-width-thin) solid var(--color-border);
  }

  .share-buttons__label {
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    font-weight: 700;
    color: var(--color-medium-gray);
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .share-buttons__group {
    display: flex;
    gap: var(--spacing-xs);
    flex-wrap: wrap;
  }

  .share-button {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 8px 16px;
    border: var(--border-width-thin) solid var(--color-border);
    border-radius: 4px;
    background-color: var(--color-white);
    color: var(--color-text);
    font-family: var(--font-sans);
    font-size: var(--font-size-sm);
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .share-button:hover {
    transform: translateY(-2px);
    box-shadow: 0 2px 8px var(--color-shadow);
  }

  .share-button:active {
    transform: translateY(0);
  }

  /* LinkedIn brand color */
  .share-button--linkedin:hover {
    background-color: #0077b5;
    color: var(--color-white);
    border-color: #0077b5;
  }

  /* Facebook brand color */
  .share-button--facebook:hover {
    background-color: #1877f2;
    color: var(--color-white);
    border-color: #1877f2;
  }

  /* Instagram brand color */
  .share-button--instagram:hover {
    background: linear-gradient(45deg, #f09433 0%, #e6683c 25%, #dc2743 50%, #cc2366 75%, #bc1888 100%);
    color: var(--color-white);
    border-color: #bc1888;
  }

  .share-button svg {
    width: 20px;
    height: 20px;
    flex-shrink: 0;
  }

  /* Mobile: hide text labels, show only icons */
  @include mobile {
    .share-button__text {
      display: none;
    }
    
    .share-button {
      padding: 8px 12px;
    }
  }

  /* Tablet and up: show text labels */
  @include tablet {
    .share-button__text {
      display: inline;
    }
  }
</style>
