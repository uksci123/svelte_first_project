<script>
  // JavaScript code 
  import "./app.css";
  import Counter from "./lib/Counter.svelte";
  let name = "Utsav";
  let lastName = "<i>Yadav</i>";
</script>

<!-- markup which is normal html -->

<!-- In the markup you can add any javaScript inside the curly braces -->
<!-- And also no need to use template literal for this  `` -->
<!-- For using the string which have HTML tag insde it will not parse it directly -->
<!-- we have to use @html  -->
<h1 class="text-7xl text-amber-400">How are you {@html name.toUpperCase() + ' ' + lastName}</h1>
<br>
<Counter maxCount={10}/>
<!-- <Counter>Yes Access the child</Counter> -->

<style lang='postcss'>
  /* All the style code to that particular componet is assigned here */
  /* Where one important fact in svelte create own thir own random class for the tag which is associated to respective componnet  */
</style> 