<script>
  let count = 0 ; 
  export let maxCount = undefined
  function increment(){
    if (count == maxCount) return ;
    count+=1 ; 
  }

  /**
   * @param {number} x
   */
  function squareCount(x){
    return x * x ;
  }

  // let string = `Your count value is ${count}`

  // This is reactive statement
  // let string  ;
  // $: if(count>6) {string = `Your count value is ${count}`}

  let string  ;
  //here you have to pass the value of the count to the funtion 
  $: {string = `Your squreCount value is ${squareCount(count)}`};
  
  let size = "large" ; 

</script>

  <!-- Normal declared variable act as state and in build handle inside the invalidate fn -->
  <button on:click={increment} class='border border-green-200 p-[2rem] mx-3' >Click Me {count}</button>
  <p class = 'text-cyan-200 text-5xl'>{string ?? ''} <br><slot>fallback Nothing is provided.</slot><slot/></p>


  
  <!-- we can use the in different manner on conditionally classing done by ternary operator 
      no in svelte provide us to use class:____={condition} -->
  <p 
    class:text-7xl={size=="large"}
  >This have to largre</p>
  



<!-- Slots slots props -->
