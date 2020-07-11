<script>
  import Title from "./Title.svelte";
  let name = "";
  let amount = null;
  $: isEmpty = !name || !amount;
  export let addExpense
  const handleSubmit = () => {
      addExpense({name, amount})
      name = ""
      amount = null
  }
</script>

<style>
  .form {
    width: 600px;
    margin: 0 auto;
  }

  .form-empty {
    color: red;
  }

  .btn {
    color: blue;
    border: 1px solid blue;
  }

  .disabled {
    color: gray;
    border: 1px solid lightgray;
  }
</style>

<section class="form">
  <Title title="Add Expense" />
  <form class="expense-form" on:submit|preventDefault={handleSubmit}>
    <div class="form-control">
      <label for="name">Name</label>
      <input type="text" id="name" bind:value={name} />
    </div>
    <div class="form-control">
      <label for="amount">Amount</label>
      <input type="number" id="amount" bind:value={amount} />
    </div>
    {#if isEmpty}
      <p class="form-empty">Please fill out all the form fields</p>
    {/if}
    <button
      type="submit"
      class="btn"
      class:disabled={isEmpty}
      disabled={isEmpty}>
      Add expense
    </button>
  </form>

</section>
