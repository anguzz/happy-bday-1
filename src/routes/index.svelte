

<script lang="ts" context="module">

</script>

<script lang="ts">
  import SEO from "svelte-seo";
  import About from "$lib/pages/Content.svelte";
  import Home from "$lib/pages/Home.svelte";
  
  import MoveConfetti from "$lib/components/ConfettiOnClick.svelte"
/* basic colors at  https://tailwindcss.com/docs/customizing-colors   more at  https://hypercolor.dev/   */ 
  let primaryBackground = "bg-gradient-to-r from-pink-300 via-purple-300 to-indigo-400";
  let neutralBackground = "bg-gradient-to-r from-indigo-300 to-purple-400";
</script>

<SEO
  title="Happy Birthday!"
  description="Digital Birthday Card for Steph"
  canonical=""
/>

<Home />
<!--About me/bio-->
<About backgroundClass={neutralBackground} />
