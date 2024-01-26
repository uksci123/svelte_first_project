<svelte:options immutable={true}/>
<!-- // this will help to component not mutate the array we have to pass the new array  -->
<script>
  // @ts-nocheck

  // JavaScript code
  import "./app.css";
  import Button from "./lib/Button.svelte";
  // import Counter from "./lib/Counter.svelte";
  // let name = "Utsav";
  // let lastName = "<i>Yadav</i>";

  import FaAngellist from "svelte-icons/fa/FaAngellist.svelte";
  import FaAllergies from "svelte-icons/fa/FaAllergies.svelte";

  import TodoList from "./lib/TodoList.svelte";
  import { v4 as uuid } from "uuid";

  let todos = [
    {
      id: uuid(),
      title: "TodoList 1",
      completed: true
    },
    {
      id: uuid(),
      title: "TodoList 2",
      completed: false
    },
    { 
      id: uuid(),
      title: "TodoList 3",
      completed: true
    },
  ];

  function handleTodo(event){
    // event.preventDefault();
    todos=[...todos,{
      id:uuid(),
      title:event.detail.title,
      completed:false
    }]
  }

  function handleToggleTodo(event){
    todos = todos.map((task)=>{
      if(task.id==event.detail.id){
        return {
          ...task,
          completed : event.detail.taskStatus
        }
      }
      return {...task};
    })
  }

  function handleRemoveTodo(event){
    todos = todos.filter((task)=>{
      if(event.detail.id != task.id || !event.detail.taskStatus){
        return task;
      }
    })
  }
</script>

<!-- markup which is normal html -->

<!-- In the markup you can add any javaScript inside the curly braces -->
<!-- And also no need to use template literal for this  `` -->
<!-- For using the string which have HTML tag insde it will not parse it directly -->
<!-- we have to use @html  -->
<!-- <h1 class="text-7xl text-amber-400">How are you {@html name.toUpperCase() + ' ' + lastName}</h1> -->
<!-- <br> -->
<!-- <Counter maxCount={10}/> -->
<!-- <Counter>Yes Access the child</Counter> -->

<Button>
  <div slot="leftContent"   let:isLeftHovered class="w-8">
    <!-- svelte-ignore missing-declaration -->
    {#if isLeftHovered}
    <FaAngellist />
    {:else}
      <FaAllergies />
    {/if}
  </div>
  Button
</Button>

<h1 class='text-5xl mb-3 ml-6'>{todos.length} Todos</h1>
<!-- <TodoList {todos} /> -->
<!-- => instead of of normal passing props it just initialse the child variable 
=> for syncronise the changes with parent component we have to bind that prop -->

<!-- <TodoList bind:todos /> -->

<!-- <button 
  class='mx-8 border border-black p-3 mb-8 rounded-lg active:translate-y-2'
  on:click={()=>{
    todos=[]
  }}
> Update to Todo
</button> -->
<!-- As you can see here the todos which is bind with TodoList component and also have 
changes with update to Todo button so how to handle this so we can move all the 
functionality of handling this form in aap.svelte so only one point of refrese to change it -->


<TodoList 
  {todos} 
  on:addTodo={handleTodo}
  on:toggleTodo={handleToggleTodo}
  on:removeTodo={handleRemoveTodo}
 />
<style lang="postcss">
  /* All the style code to that particular componet is assigned here */
  /* Where one important fact in svelte create own thir own random class for the tag which is associated to respective componnet  */
</style>
