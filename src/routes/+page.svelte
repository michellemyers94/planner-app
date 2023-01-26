<script>
    import Todos from "../components/Todos.svelte";
    import './styles.css';

    let todos = [
        { id: 1, name: "Complete Assignment 1", completed: true },
        { id: 2, name: "Complete Assignment 2", completed: true },
        { id: 3, name: "Complete Assignment 3", completed: false }
    ];
</script>


<div class="grid-container">

<!--    left column-->
    <div class="nav-column">

        <h1 class="app-title">Planner App</h1>
        <h3 class="categories-title">categories</h3>


        <div class="category-buttons">
        <button class="add-category">+ add category</button>
        <button class="edit-category">- edit category</button>
            </div>
    </div>



<!--    right column-->
    <div class="main-body">
        <h1>Task Overview</h1>
        <Todos {todos} />
    </div>




</div>
