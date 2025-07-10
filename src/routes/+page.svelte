<script>
    /** @type {{ data: import('./$types').PageData }} */
    let { data } = $props();

    import AddTask from './AddTask.svelte';
    import TaskListItem from './TaskListItem.svelte';

    let tasks = $state([])
    $inspect(tasks)

    function modifyTask(task){
        console.log('modifyTask running for : ')
        console.log(task)
        tasks.forEach(element => {
            if(element.id == task.id){
                element = task
                return
            }
        });
        saveToStorage()
    }

    let currentlyEditing = $state('')
    function editingMode(taskId){
        currentlyEditing = taskId
    }

    function deleteTask(taskId){
        tasks = tasks.filter(task => task.id != taskId)
        saveToStorage()
    }

    function saveToStorage(){
        localStorage.setItem('tasks', JSON.stringify(tasks))
    }

    $effect(() => {
        let myTasks = localStorage.getItem('tasks')
        if (myTasks){
            tasks = JSON.parse(myTasks)
        }
    })

</script>

<div class="w-screen h-screen bg-slate-900 overflow-scroll overflow-x-hidden flex flex-col">
    <AddTask {tasks} {saveToStorage}/>

    {#each tasks as task}
        {#if task.finished == false}
            <TaskListItem {task} {modifyTask} {editingMode} {currentlyEditing} {deleteTask}/>
        {/if}
    {/each}

    {#each tasks as task}
        {#if task.finished == true}
            <TaskListItem {task} {modifyTask} {editingMode} {currentlyEditing} {deleteTask}/>
        {/if}
    {/each}



</div>