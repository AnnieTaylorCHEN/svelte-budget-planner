<script>
  import { setContext } from "svelte";
  import Navbar from "./Navbar.svelte";
  import Form from './Form.svelte';
  import Totals from "./Totals.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import expensesData from "./expenses";

  let expenses = [...expensesData];
  $: total = expenses.reduce((acc, curr) => { 
    return acc += curr.amount;
  }, 0)
  
  const removeExpense = id => {
    expenses = expenses.filter(item => item.id !== id);
  };
  setContext("remove", removeExpense);
  const clearAllExpenses = () => {
    expenses = [];
  };

  const addExpense = ({ name, amount}) => {
    let expense = {
      id: Math.random() * Date.now(),
      name,
      amount,
    }
    expenses = [expense, ...expenses]
  }
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

    .clear-all {
      padding: 1rem 2rem;
      color: white;
      background: red;
    }
  }
</style>

<Navbar />
<Form {addExpense} />
<Totals title="All your expenses" {total} />
<main>
  <ExpensesList {expenses} />
  <button class="clear-all" on:click={clearAllExpenses}>
    Clear All Expenses
  </button>
</main>
