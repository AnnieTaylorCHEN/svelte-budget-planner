<script>
  import { setContext, onMount } from "svelte";
  import Navbar from "./Navbar.svelte";
  import Form from "./Form.svelte";
  import Totals from "./Totals.svelte";
  import ExpensesList from "./ExpensesList.svelte";
  import Modal from "./Modal.svelte";
  import expensesData from "./expenses";

  let expenses = [...expensesData];
  let setName = "";
  let setAmount = null;
  let setId = null;
  let isFormOpen = false;

  $: isEditing = setId ? true : false;

  $: total = expenses.reduce((acc, curr) => {
    return (acc += curr.amount);
  }, 0);

  const showForm = () => {
    isFormOpen = true;
  };

  const hideForm = () => {
    isFormOpen = false;
    setId = null;
    setName = "";
    setAmount = null;
  };

  const removeExpense = id => {
    expenses = expenses.filter(item => item.id !== id);
    setLocalStorage();
  };

  const clearAllExpenses = () => {
    expenses = [];
    setLocalStorage();
  };

  const addExpense = ({ name, amount }) => {
    let expense = {
      id: Math.random() * Date.now(),
      name,
      amount
    };
    expenses = [expense, ...expenses];
    setLocalStorage();
  };

  const setModifiedExpense = id => {
    let expense = expenses.find(item => item.id === id);
    setId = expense.id;
    setName = expense.name;
    setAmount = expense.amount;
    showForm();
  };

  const editExpense = ({ name, amount }) => {
    expenses = expenses.map(item => {
      return item.id === setId ? { ...item, name, amount } : { ...item };
    });
    setId = null;
    setName = "";
    setAmount = null;
    setLocalStorage();
  };

  setContext("remove", removeExpense);
  setContext("edit", setModifiedExpense);

  const setLocalStorage = () => {
    localStorage.setItem(
      "AnnieBudgetPlannerExpenses",
      JSON.stringify(expenses)
    );
  };

  onMount(() => {
    expenses = localStorage.getItem("AnnieBudgetPlannerExpenses")
      ? JSON.parse(localStorage.getItem("AnnieBudgetPlannerExpenses"))
      : [];
  });
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

<Navbar {showForm} />
{#if isFormOpen}
  <Modal>
    <Form
      {addExpense}
      name={setName}
      amount={setAmount}
      {isEditing}
      {editExpense}
      {hideForm} />
  </Modal>
{/if}
<Totals title="All your expenses" {total} />
<main>
  <ExpensesList {expenses} />
  <button class="clear-all" on:click={clearAllExpenses}>
    Clear All Expenses
  </button>
</main>
