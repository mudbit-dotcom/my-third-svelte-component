<!--
@component
AuthorBio.svelte — Author Biography Box

Displays author information with photo, name, title, and social media links.
Ideal for article bylines, about sections, or team pages.

USAGE EXAMPLE:
<AuthorBio
  name="Niya Doyle"
  title="Culture Writer & Reporter"
  photo="/niya.jpg"
  bio="Niya Doyle is a Brooklyn-based freelance writer covering culture and beauty. Her work has appeared in TeenVogue, Dazed Beauty, Autostraddle, Haloscope Mag, and more! When she’s not writing, she’s scrolling through Depop for the latest thrifted finds. Check out her bylines below!"
  twitter="niyadoyle"
  linkedin="https://www.linkedin.com/in/niya-doyle/"
  email="niyadoyle@gmail.com"
/>
-->
<script>
  import { asset } from '$app/paths';
  
  let {
    name,                   // Required: Author's full name
    title = '',             // Optional: Job title or role
    photo = '',             // Optional: Author photo URL
    bio = '',               // Optional: Short biography
    twitter = '',           // Optional: Twitter/X username (without @)
    linkedin = '',          // Optional: LinkedIn profile URL or username
    email = '',             // Optional: Contact email
    website = '',           // Optional: Personal website URL
  } = $props();

  // Resolve local images
  const resolvedPhoto = $derived(
    photo && photo.startsWith('/') && !photo.startsWith('//') 
      ? asset(photo) 
      : photo
  );
</script>

<aside class="author-bio">
  <div class="author-bio__content">
    {#if photo}
      <div class="author-bio__photo">
        <img 
          src={resolvedPhoto} 
          alt={name}
          class="author-bio__img"
        />
      </div>
    {/if}
    
    <div class="author-bio__info">
      <h3 class="author-bio__name">{name}</h3>
      {#if title}
        <p class="author-bio__title">{title}</p>
      {/if}
      {#if bio}
        <p class="author-bio__text">{bio}</p>
      {/if}
      
      {#if twitter || linkedin || email || website}
        <div class="author-bio__social">
          {#if twitter}
            <a 
              href="https://twitter.com/{twitter}" 
              target="_blank" 
              rel="noopener noreferrer"
              class="social-link"
              aria-label="Twitter profile"
            >
              <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true">
                <path fill="currentColor" d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/>
              </svg>
            </a>
          {/if}
          
          {#if linkedin}
            <a 
              href={linkedin.startsWith('http') ? linkedin : `https://linkedin.com/in/${linkedin}`}
              target="_blank" 
              rel="noopener noreferrer"
              class="social-link"
              aria-label="LinkedIn profile"
            >
              <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true">
                <path fill="currentColor" d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
              </svg>
            </a>
          {/if}
          
          {#if email}
            <a 
              href="mailto:{email}"
              class="social-link"
              aria-label="Email contact"
            >
              <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true">
                <path fill="none" stroke="currentColor" stroke-width="2" d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                <polyline fill="none" stroke="currentColor" stroke-width="2" points="22,6 12,13 2,6"/>
              </svg>
            </a>
          {/if}
          
          {#if website}
            <a 
              href={website}
              target="_blank" 
              rel="noopener noreferrer"
              class="social-link"
              aria-label="Personal website"
            >
              <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true">
                <circle cx="12" cy="12" r="10" fill="none" stroke="currentColor" stroke-width="2"/>
                <line x1="2" y1="12" x2="22" y2="12" fill="none" stroke="currentColor" stroke-width="2"/>
                <path fill="none" stroke="currentColor" stroke-width="2" d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/>
              </svg>
            </a>
          {/if}
        </div>
      {/if}
    </div>
  </div>
</aside>

<style lang="scss">
  .author-bio {
    background-color: var(--color-background-secondary, #f8f9fa);
    border: 1px solid var(--color-border, #e1e4e8);
    border-radius: 8px;
    padding: 1.5rem;
    margin: 2rem 0;
    
    &__content {
      display: flex;
      gap: 1.25rem;
      align-items: flex-start;
    }
    
    &__photo {
      flex-shrink: 0;
    }
    
    &__img {
      width: 80px;
      height: 80px;
      border-radius: 50%;
      object-fit: cover;
      border: 2px solid var(--color-border, #e1e4e8);
    }
    
    &__info {
      flex: 1;
      min-width: 0; // Allow text to wrap properly
    }
    
    &__name {
      margin: 0 0 0.25rem 0;
      font-size: 1.25rem;
      font-weight: 700;
      color: var(--color-text-primary, #1a1a1a);
      line-height: 1.3;
    }
    
    &__title {
      margin: 0 0 0.75rem 0;
      font-size: 0.9rem;
      color: var(--color-text-secondary, #666);
      font-weight: 500;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }
    
    &__text {
      margin: 0 0 1rem 0;
      font-size: 0.95rem;
      line-height: 1.6;
      color: var(--color-text-primary, #333);
    }
    
    &__social {
      display: flex;
      gap: 0.75rem;
      align-items: center;
    }
  }
  
  .social-link {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 36px;
    height: 36px;
    border-radius: 50%;
    background-color: var(--color-background-tertiary, #fff);
    border: 1px solid var(--color-border, #e1e4e8);
    color: var(--color-text-secondary, #666);
    transition: all 0.2s ease;
    text-decoration: none;
    
    &:hover {
      background-color: var(--color-primary, #0066cc);
      border-color: var(--color-primary, #0066cc);
      color: white;
      transform: translateY(-2px);
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
    }
    
    &:focus {
      outline: 2px solid var(--color-primary, #0066cc);
      outline-offset: 2px;
    }
    
    svg {
      display: block;
    }
  }
  
  // Responsive layout
  @media (max-width: 480px) {
    .author-bio {
      padding: 1rem;
      
      &__content {
        flex-direction: column;
        align-items: center;
        text-align: center;
      }
      
      &__img {
        width: 100px;
        height: 100px;
      }
      
      &__social {
        justify-content: center;
      }
    }
  }
</style>
