<script>
  import { setContext } from "svelte";
  import Navbar from "./Navbar.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import expensesData from "./expenses";

  let expenses = [...expensesData];
  const removeExpense = id => {
    expenses = expenses.filter(item => item.id !== id);
  };
  setContext("remove", removeExpense);
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<Navbar />
<main>
  <ExpensesList {expenses} />
</main>
