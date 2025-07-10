<script>
    const { task, modifyTask, editingMode, currentlyEditing, deleteTask } = $props()
    let editMode = $derived(task.id == currentlyEditing)
    let textInEditMode = $state(task.text)

    function finishBtnClicked(){
        let tempTask = task
        tempTask.finished = true
        modifyTask(tempTask)
    }

    function unfinishBtnClicked(){
        let tempTask = task
        tempTask.finished = false
        modifyTask(tempTask)
    }

    function saveBtnClicked(){
        editingMode('')
        let tempTask = task
        tempTask.text = textInEditMode
        modifyTask(tempTask)
    }
</script>

<div class="flex justify-center my-3 items-center transition-all duration-800 {task.finished ? 'bg-slate-800/60' : 'bg-slate-800/100'}">
    {#if editMode == false}
        <div class="w-[80%] px-5 py-2 {task.finished ? 'text-stone-400/60' : 'text-stone-200/80'}">{task.text}</div>
    {:else}
        <input type="text" class="w-[75%] px-5 py-2 my-1 mx-2 rounded-3xl bg-slate-700/90 text-slate-200" bind:value={textInEditMode}/>
    {/if}

    <!-- Edit Btn -->
    {#if editMode == false}
        <!-- <button onclick={() => editMode = true}> -->
        <button onclick={() => editingMode(task.id)}>
            <img class='w-[1.7em] h-[1.7em] pb-1 pl-1 mx-1 filter invert-50 hover:scale-120 hover:invert-70' alt='edit' src='https://cdn-icons-png.flaticon.com/512/1827/1827933.png' />
        </button>
    {/if}

    <!-- SaveEdits Btn -->
    {#if editMode == true}
        <button onclick={saveBtnClicked}>
            <img class='w-[1.7em] h-[1.7em] pb-1 pl-1 mx-1 invert-50 hover:scale-120 hover:invert-70' alt='edit' src='https://cdn-icons-png.flaticon.com/512/2874/2874050.png' />
        </button>
    {/if}

    <!-- Delete Btn -->
    {#if editMode == true}
        <button onclick={() => deleteTask(task.id)}>
            <img class='w-[1.7em] h-[1.7em] pb-1 pl-1 mx-1 invert-50 hover:scale-120 hover:invert-70' alt='edit' src='https://cdn-icons-png.flaticon.com/512/3221/3221845.png' />
        </button>
    {/if}
    
    <!-- Unfinish Btn -->
    {#if task.finished==true && editMode != true}
        <button onclick={unfinishBtnClicked}>
            <img class='w-[1.6em] h-[1.6em] ml-2 mr-[0.4em] mx-1  invert-50 hover:scale-120 hover:invert-70' alt='finished' src='https://cdn-icons-png.flaticon.com/512/25/25643.png' />
        </button>

    <!-- Finish Btn -->
    {:else if task.finished==false && editMode != true} 
        <button onclick={ finishBtnClicked}>
            <img class='w-[2em] h-[2em] invert-50 mx-1 hover:scale-120 hover:invert-70' alt='unfinished' src='https://cdn-icons-png.flaticon.com/512/8924/8924271.png' />
        </button>
    {/if}
     
    
    
</div>