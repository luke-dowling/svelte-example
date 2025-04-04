<script lang="ts">
  import type { Snippet } from "svelte";

  let {
    name,
    children,
    secondChild,
  }: {
    name: string;
    children: Snippet;
    secondChild: Snippet<[text: string]>;
  } = $props();
</script>

<div>
  <h1>{name ? name : "User"}'s Form</h1>

  {@render children()}
  <h3>{@render secondChild("John")}</h3>
</div>

<style></style>
