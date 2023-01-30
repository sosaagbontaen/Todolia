<!-- This code was partially produced by following a To-do app tutorial by "Svelte Mastery" -->

<script>
	let name = "";
	let taskCount = 0;
	let tasks = [];
	let taskLimit = 5;
	let fav_color = '#ff3e00';

    //Adds a new task to the to-do list
    function pushTask(){
		//Software Concept : Control Flow
		//Check if task limit has been reached
		if (taskCount == taskLimit){
			//Software Concept : Formatted String
			alert('Limit of ' + taskLimit + ' tasks reached');
		}
		else{
			//Initialize a new empty task
			tasks = [...tasks, ''];
			taskCount++;
		}
    }
    //Removes a task from the to-do list
    function popTask(index){
		tasks = [...tasks.slice(0, index), ...tasks.slice(index+1)];
		taskCount--;
    }
</script>


<main style = "--theme-color: {fav_color}">
	<!--Software Concept : Control Flow-->
	{#if name == ""}
		<h1>Todolia</h1>
	{:else}
	<!--Software Concept : Formatted String-->
		<h1>Welcome {name}!</h1>
	{/if}
	<p>What is your name?</p>
	<!--Software Concept : Reactive Values-->
	<input bind:value={name}>
	<p>What is your favorite color (hex code)?</p>
	<!--Software Concept : Reactive Values-->
	<input type="color" bind:value={fav_color} style="height: 50px;">
	
	<!--Software Concept : Control Flow-->
	{#if taskCount > 1}
		<!--Software Concept : Reactive Values-->
		<!--Software Concept : Formatted String-->
		<p>You currently have {taskCount} tasks!</p>
	{:else if taskCount == 1}
		<p>You currently have 1 task!</p>
	{:else}
		<p>Click '+' to create a new task!</p>
	{/if}
	
	<!--Software Concept : Control Flow-->
	<!-- Loop through each task in array and display them as textboxes -->
	{#each tasks as task, index}
		<input bind:value={tasks[index]}>
		<button on:click={()=>popTask(index)}>x</button><br>
	{/each}

<button on:click={pushTask}>+</button>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
		background-color: var(--theme-color);;
	}

	h1 {
		color: #ffffff;
		text-transform: uppercase;
		font-size: 3.5em;
		font-weight: 100;
	}
	p{
		color: #ffffff
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
