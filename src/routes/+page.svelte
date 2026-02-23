<!--
@component
This is your page!
-->
<script>
  // Import all the news furniture components
  import ArticleHeader from '$lib/components/ArticleHeader.svelte';
  import ArticleBody from '$lib/components/ArticleBody.svelte';
  import Image from '$lib/components/Image.svelte';
  import RelatedLinks from '$lib/components/RelatedLinks.svelte';
  import EditorNote from '$lib/components/EditorNote.svelte';
  import ShareButtons from '$lib/components/ShareButtons.svelte';
  import AuthorBio from '$lib/components/AuthorBio.svelte';
 

  // Article metadata
  let headline = 'Become a force for good. Join our next class.';
  let byline = 'Niya Doyle';
  let pubDate = '2026-02-22';

  // Related stories
  const relatedStories = [
    { headline: 'Behind the scences at NYFW', href: 'https://girlsunited.essence.com/feedback/news/painted-by-esther/' },
    { headline: 'An interview with a beauty expert', href: 'https://girlsunited.essence.com/beauty/the-reality-behind-the-decline-of-black-owned-beauty-funding/' },
    { headline: "Wicked Movie beauty shopping guide", href:"https://girlsunited.essence.com/beauty/wicked-for-ggod-beauty-products/"},
  ];
</script>

<!-- This sets the page title in the browser tab -->
<svelte:head>
  <title>{headline} | NYCity News Service</title>
  <meta name="description" content="At the Craig Newmark Graduate School of Journalism at the City University of New York, change is in our DNA. That comes of being born in 2006, as the digital revolution was transforming our profession in ways none of us could have imagined." />
</svelte:head>

<!-- Your page content goes here -->
<div class="container">
  
  <!-- Article Header: Headline, byline, and publication date -->
  <ArticleHeader
    {headline}
    {byline}
    {pubDate}
  />

  <!-- Lead Image: Animated gif of students at the journalism school -->
 <Image
  src="/niya.JPG"
  alt="picture of niya doyle"
  caption="Niya Doyle's photo"
  credit="Niya Doyle / The Daily News"
  size="large"
/>

  <!-- Article Body: The main story text with proper typography -->
  <ArticleBody>
    <p>
Winter is upon us, and with the dizzying amount of serums, moisturizers, and acids available it’s hard to keep up with what’s right for your skin. Essence Girls United spoke to board-certified dermatologist Dr. Mara Weinstein Velez, M.D at the University of Rochester Medical Center about how to keep your skin moisturized and healthy during the cooler months.
    </p>
    Q: Let’s start with the basics. What products do you need during the winter months?
    <p>
    <p>
Dr. Velez: ​​I believe that there should be at least two routines. First thing in the morning. I recommend cleansing with a hydrating cleanser. So if you’re super oily, then you can stick to like gel, but something that’s not too drying. I would transition from your gel or foaming cleanser to a hydrating cleanser, so that would be like more of a creamy cleanser.
    </p>

  </ArticleBody>

<AuthorBio
  name="Niya Doyle"
  title="Culture Writer & Reporter"
  photo="/niya.JPG"
  bio="Niya Doyle is a Brooklyn-based freelance writer covering culture and beauty. Her work has appeared in TeenVogue, Dazed Beauty, Autostraddle, Haloscope Mag, and more! When she’s not writing, she’s scrolling through Depop for the latest thrifted finds. Check out her bylines below!"
  twitter="niyadoyle"
  linkedin="https://www.linkedin.com/in/niya-doyle/"
  email="niyadoyle@gmail.com"
/>

  <EditorNote>
 <p>This article was updated November 13th, 2025 to include new information.</p>
</EditorNote>
  <!-- Related Stories: Links to other articles -->
  <RelatedLinks
    title="Related Stories"
    links={relatedStories}
  />

<ShareButtons 
  url="https://example.com/article" 
  title="Article Title"
/>

</div>

<style>
  /* Styles here only apply to this page */
  .container {
    padding: var(--spacing-lg) var(--spacing-md);
  }
</style>