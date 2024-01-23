<script>
// @ts-nocheck
    import {v4 as uuid} from 'uuid';
    import Button from "./Button.svelte";
    import { createEventDispatcher } from 'svelte';

    // Todo List 
    export let todos = [];

    let inputText = '';
    // function handleAddTodo(){
    //     todos = [...todos, {
    //         id: uuid(),
    //         title : inputText
    //     }]
    //     console.log(inputText);
    //     inputText = '';
    // } 
    // handle the changes in parent componet we just call 
    // custom even from child componet   

    const dispatch = createEventDispatcher();
    function handleAddTodo(){
        const isCanceled = dispatch('addTodo' , {
            title : inputText
        },{
            cancelable:true
        })
        // take two argument first function name , pass value to it
        if(isCanceled){
            console.log(inputText)
            inputText='';
        }
    }

    // if want to do some stuff on passing preventDefault in parent and cancel the 
    // dispatch fucntion then pass as argugent and then 
    // dispatch return true or fase if preventDefault use in the handleTodo

    function handleToggleTodo( id , taskStatus){
        dispatch('toggleTodo',{
            id,
            taskStatus
        })
    }

    function handleRemoveTodo(id){
        dispatch('removeTodo',{
            id
        })
    }
</script>
<div>
    <ul class = 'px-12'>
        {#each todos as todo , index (todo.id)}
            {@const number = index + 1}
            <li class='mb-3'>
                <input 
                on:input={(event)=>{
                    event.currentTarget.checked = todo.completed
                    console.log(todo.completed)
                    handleToggleTodo(todo.id , !todo.completed)
                }} 
                checked={todo.completed}
                type=checkbox/>
                {todo.title}
                <button 
                    class='border border-black rounded-lg p-1 active:translate-y-2'
                    on:click={()=>handleRemoveTodo(todo.id)}
                    >remove</button>
            </li>
        {/each} 
    </ul>
    <!-- bind:this={intput} is not workint might we in the previous version or setting -->
    <!-- {inputText} -->
    <form on:submit|preventDefault={handleAddTodo}>
        <!-- <input 
            type = "text" 
            class='border border-black rounded-lg relative top-[15px] left-[32px]'
            on:input={(e)=>{
                inputText = e.target.value
            }}
        /> -->
        <input 
        type = "text" 
        class='border border-black rounded-lg pl-2 relative top-[15px] left-[32px]'
        bind:value={inputText}
    />
        <Button type="submit">Add</Button>
    </form>
</div>
