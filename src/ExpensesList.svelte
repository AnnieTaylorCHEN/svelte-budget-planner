<script>
  import SectionTitle from "./Title.svelte";
  import Expense from "./Expense.svelte";
  export let expenses = [];
</script>

<style>
  h2 {
    color:blue;
  }
</style>

<section>
  <SectionTitle title="Expense List" />
  <ul>
    {#each expenses as expense}
      <Expense {...expense} />
    {:else}
      <h2>Currently no expenses, add some?</h2>
    {/each}
  </ul>
</section>
