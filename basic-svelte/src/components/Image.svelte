<script lang="ts">
  let src = "/image.gif";
  let alt = "rick roll image";
  let { index } = $props();
  $effect(() => {
    console.log(`Index changed to: ${index}`);
  });
</script>

<img {src} {alt} />

<style>
  img {
    max-width: 100%;
    height: auto;
    border-radius: 10px;
    box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.5);
    transition: all 0.3s ease;
  }

  img:hover {
    transform: scale(1.05);
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.5);
  }
</style>
