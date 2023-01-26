

<script>
    import Swal from "sweetalert2";


export let todos = [];
$: totalTodos = todos.length;
$: completedTodos = todos.filter((todo) =>
    todo.completed).length;

function removeTodo(todo) {
    todos = todos.filter((t) => t.id !== todo.id)
}



let newTodoName = ''

function addTodo() {
    todos = [...todos, { id: newTodoId, name: newTodoName, completed: false }]
    newTodoName = ''
}


let newTodoId
$: {
    if (totalTodos === 0) {
        newTodoId = 1;
    } else {
        newTodoId = Math.max(...todos.map((t) => t.id)) + 1;
    }
}



let filter = 'all'
const filterTodos = (filter, todos) =>
    filter === 'active' ? todos.filter((t) => !t.completed) :
        filter === 'completed' ? todos.filter((t) => t.completed) :
            todos

</script>

<form on:submit|preventDefault={addTodo}>
<div class="task-block">




<!--add task    -->

    <h2 id="list-heading">{completedTodos} out of {totalTodos} items completed</h2>


<div class="tab">
    <h4 class="tab-title">
        OSU Courses
    </h4>
    </div>
    <ul class="task-block">
        {#each todos as todo (todo.id)}

            <li class="todo">
                <input type="checkbox" class="checkmark" id="todo-{todo.id}"
                       on:click={() => todo.completed = !todo.completed}
                       checked={todo.completed}
                />

                <label for="todo-{todo.id}" class="">
                    {todo.name}
                </label>

            <div class="edit-delete-item-group">
                <button type="button" class="edit-task">edit</button>
                <button type="button" class="delete-task"
                        on:click={() => {
                                Swal.fire({
                                  title: 'Are you sure you want to delete this task?',
                                  text: 'There\'s no going back!',
                                  icon: 'warning',
                                  showCancelButton: true,
                                  confirmButtonText: 'Yes, delete it!',
                                  cancelButtonText: 'No, keep it'
                                }).then(result => {
                                  if (removeTodo(todo)) {
                                    Swal.fire('Deleted!', 'Your imaginary file has been deleted.', 'success');
                                  } else if (result.dismiss === Swal.DismissReason.cancel) {
                                    Swal.fire('Cancelled', 'Your imaginary file is safe :)', 'error');
                                  }
                                });
                              }}>
                    delete
                </button>

            </div>
            </li>

            {:else}
            <li>Add a task to get started!</li>
            {/each}

    </ul>




<div class="add-task-area">
    <input bind:value={newTodoName}
           type="text"
           id="todo-0"
           autocomplete="off"
           class="" />
    <button type="submit" disabled="" class="add-task">
        + add task
    </button>
    </div>
</div>
</form>

