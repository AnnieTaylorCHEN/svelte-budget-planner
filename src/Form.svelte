<script>
  import Title from "./Title.svelte";
  export let name = "";
  export let amount = null;
  export let isEditing;
  export let editExpense;
  export let addExpense;
  export let hideForm;
  $: isEmpty = !name || !amount;
  const handleSubmit = () => {
    if (isEditing) {
      editExpense({ name, amount });
    } else {
      if (name !== "" && amount !== null) {
        addExpense({ name, amount });
      }
      name = "";
      amount = null;
      hideForm();
    }
  };
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

  .btn--close {
    color: red;
    border: 1px solid red;
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
      {#if isEditing}Edit Expense{:else}Add Expense{/if}
    </button>
    <button class="btn--close" on:click={hideForm}>Close Form</button>
  </form>

</section>
