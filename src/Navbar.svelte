<script>
  export let showForm;
</script>

<style>
  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
    text-align: center;
  }

  .add-btn {
    display: block;
    margin: 0 auto;
  }
</style>

<nav>
  <h1>Annie's Budget Planner</h1>
  <button class="add-btn" on:click={showForm}>Add item</button>
</nav>
