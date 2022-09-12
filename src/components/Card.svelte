<script>

	import { onMount } from 'svelte';
	import    axios    from 'axios';

 
	let loading  = true;
	let isFemale = false;
	let name     = '';
	let phone    = '';
	let email    = '';
	let gender   = '';
	let picture  = '';


	const getUser = () => {

		loading = true;

		axios.get( 'https://randomuser.me/api/' ).then( response => {

			let user = response.data.results[0];

			name     = user.name.first + ' ' + user.name.last;
			phone    = user.phone;
			email    = user.email;
			gender   = user.gender;
			picture  = user.picture.large;

			( user.gender === 'female' ) ? isFemale = true : isFemale = false;

			loading = false;

		});

	}

	onMount(async () => {

		getUser();

	});

</script>


<div class="row">

	<div class="col-md-4"></div>

	<div class="col-md-4 card p-4 text-center { isFemale === true ? 'pink0' : 'blue0' } { loading === true ? 'loading' : '' }" style="height: 400px;">

		<div class="card-top p-4">

			<img class="rounded-circle" src={picture} alt="" />

		</div>

		<div class="card-title h4">{ name }</div>

		<div class="card-title h6 mt-2">{ phone }</div>

		<div class="card-title h6 mt-2">{ email }</div>

		<button class="btn mt-4  { isFemale === true ? 'pink' : 'blue text-light' }" on:click={getUser}>Randomize</button>

	</div>

	<div class="col-md-4"></div>

</div>


<style scoped>

	.pink0 {

		background-color: rgba(255, 194, 204, .1);

	}

	.pink {

		background-color: pink;

	}

	.blue0 {

		background-color: rgba(13, 110, 253, .1);
		
	}

	.blue {

		background-color: #0d6efd;
		
	}

	.loading {

		opacity: .3;
		
	}

</style>
