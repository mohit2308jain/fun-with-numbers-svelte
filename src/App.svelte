<script>
	import { Input, Button, Label } from 'sveltestrap';
	import axios from 'axios';
	import { onMount } from 'svelte'
	let inputNumber = null;
	let data;

	/*
	onMount(
		async () => {
			data = await fetch(`http://numbersapi.com/42`).then(x => console.log(x))
		}
	)
	*/

	const submitNumber = async(number) => {
		console.log(number)
		if(!number){
			alert('Please Enter a number..');
		}
		else{
			await axios.get(`http://numbersapi.com/${number}`).then(x => data = x.data);
		}
	}
	
</script>


<div class="container">
	<div class="row">
		<div class="col-12">
			<Label for="exampleNumber">Number</Label>
			<Input type="number" name="number" bind:value={inputNumber}
			id="exampleNumber" placeholder="Enter a number.." />
		</div>
	</div>
	<div class="row">
		<div class="col-12">
			{#if (inputNumber)}
				<h5>{inputNumber}</h5>
			{:else}
				<h5>Please enter a number in above input field.</h5>
			{/if}
		</div>
	</div>
	<div class="row">
		<div class="col-12">
			<Button on:click={submitNumber(inputNumber)} color="danger">Submit</Button>
		</div>
	</div>
	<div class="row">
		<div class="col-12">
			{#if (data)}
				<h1>{JSON.stringify(data)}</h1>
			{:else}
				<h4>Not Fetched</h4>
			{/if}
		</div>
	</div>
</div>

<style>
	
</style>