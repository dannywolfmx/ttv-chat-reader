<script lang="ts">
   import { onMount } from "svelte";

   export let message: string = "";
   let embedUrl: string = "";

   const extractYoutubeURL = (message: string) => {
      const youtubeRegex =
         /(?:https?:\/\/)?(?:www\.)?(?:youtube\.com|youtu\.be)\/(?:watch\?v=)?(.+)/g;
      const youtubeMatch = message.match(youtubeRegex);
      if (youtubeMatch) {
         let url = youtubeMatch[0];
         embedUrl = url.replace("watch?v=", "embed/");
      } else {
         embedUrl = "";
      }
   };

   $: if (message) {
      extractYoutubeURL(message);
   }
</script>

{#if embedUrl !== ""}
   <main>
      <iframe
         title="video player"
         src={embedUrl}
         frameborder="0"
         allowfullscreen
      />
   </main>
{/if}
