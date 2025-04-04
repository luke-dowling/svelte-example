<script lang="ts">
  import Header from "./components/Header.svelte";
  let formState = $state({
    name: "",
    birthday: "",
    step: 0,
    error: "",
  });
  const QUESTIONS = [
    {
      question: "What is your name?",
      id: "name",
      type: "text",
    },
    {
      question: "What is your birthday?",
      id: "bday",
      type: "date",
    },
  ];
</script>

<Header name={formState.name}>
  <p>Hello</p>
  {#snippet secondChild(name)}
    <p>Second Child: {name}</p>
  {/snippet}
</Header>

<main>
  <p>Step: {formState.step + 1}</p>

  <!-- {#each QUESTIONS as question (question.id)} -->
  {#each QUESTIONS as question (question.id)}
    {@render formStep(question)}
  {/each}
  <!-- {#each QUESTIONS as { id, question, type } (id)}
    {@render formStep({
      question,
      id,
      type,
    })}
  {/each} -->

  {#if formState.error}
    <p class="error">{formState.error}</p>
  {/if}
</main>

<!-- snippets -> reusable code templates -->
{#snippet formStep({
  question,
  id,
  type,
}: {
  type: string;
  question: string;
  id: string;
})}
  <article>
    <div>
      <label for={id}>{question}</label>
      <input {type} {id} bind:value={formState[id]} />
    </div>
  </article>
{/snippet}

<style>
  .error {
    color: red;
  }
</style>
