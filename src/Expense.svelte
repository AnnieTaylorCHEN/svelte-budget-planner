<script>
  import { getContext } from "svelte";
  export let id;
  export let name = "";
  export let amount = 0;
  export let displayAmount = false;
  const toggleAmount = () => {
    displayAmount = !displayAmount;
  };

  const removeExpense = getContext("remove");
  const setModifiedExpense = getContext("edit");
</script>

<style>
  .expense-card {
    display: flex;
    justify-content: space-between;
    margin: 0 auto;
    max-width: 800px;
    padding: 1rem;
    border-bottom: 1px solid blue;
  }
  .edit,
  .delete,
  .details {
    font-size: 0.6rem;
  }

  .delete {
    color: red;
  }
</style>

<article class="expense-card">
  <div class="expense-info">
    <h2>
      {name}
      <button class="details" on:click|once={toggleAmount}>details</button>
    </h2>
    {#if displayAmount}
      <h4>$ {amount}</h4>
    {/if}

  </div>
  <div class="expense-btn">
    <button class="edit" on:click={() => setModifiedExpense(id)}>edit</button>
    <button class="delete" on:click={() => removeExpense(id)}>delete</button>
  </div>
</article>
