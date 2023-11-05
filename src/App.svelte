<script>
    import SignUpPage from "../pages/SignUpPage.svelte";
	import {registrationState} from "../stores/store";
	import PersonalityQuiz from "../pages/PersonalityQuizContainer.svelte";
	import Dashboard from "../pages/Dashboard.svelte";
	import AvatarCreation from "../pages/AvatarCreation.svelte";

	let resultsString = '';
	let avatarURL = '';
	let username = '';
	let newUser = false;

	const API_ENDPOINT = "http://54.210.73.216:"

	function handleQuizFinish(event) {
		resultsString = event.detail.results;
		console.log('Received quiz results:', resultsString);
	}

	function handleSignUpFinish(event) {
		username = event.detail.name;
		console.log("User name is", event.detail.name)
		if (event.detail.new) {
			newUser = true;
		}
	}

	async function handleAvatarCreationFinish(event) {
		console.log("HELLO")
		if(newUser) {
			console.log("HEY THERE")
			avatarURL = event.detail.url;
			console.log(avatarURL)
			// Make request to register user, you have all the neccesary data
			await registerUser(username, resultsString, avatarURL)
		}
		
		registrationState.update(state => ({...state, showAvatarCreation: false, showDashboard: true}))
	}

	async function registerUser(username, personality_data, avatar_url) {
		// Construct the payload
		const payload = {
			username: username,
			personality_data: personality_data,
			avatar_url: avatar_url
		};

		console.log(JSON.stringify(payload))
		// Set up the options for the fetch call
		const requestOptions = {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify(payload) // Convert the payload into a JSON string
		};

		try {
			// Perform the POST request to the /register_user endpoint
			const response = await fetch(`${API_ENDPOINT}${7060}/register_user`, requestOptions);
			console.log(response)
			// If the response is ok, handle the data
			if (response.ok) {
				const responseData = await response.json();
				// Process the data received from the server
				console.log('User registered:', responseData);
				
			} else {
				// If the response is not ok, throw an error with the status
				const error = new Error(`HTTP error! status: ${response.status}`);
				console.error(error);
				// Handle the error accordingly in your UI
				throw error;
			}
		} catch (error) {
			// Handle the error from the fetch operation
			console.error('There was a problem with the fetch operation:', error.message);
			throw error;
		}
	}


	$: if($registrationState.showDashboard){
		// retrieve user_data
	}

</script>

<main>
	{#if $registrationState.showSignUpPage}
  		<SignUpPage on:finish={handleSignUpFinish} />
	{/if}
	{#if $registrationState.showPersonalityQuiz}
  		<PersonalityQuiz on:finish={handleQuizFinish} />
	{/if}
	{#if $registrationState.showAvatarCreation } 
		<AvatarCreation on:finish={handleAvatarCreationFinish}/>
	{/if}
	{#if $registrationState.showDashboard}
  		<Dashboard />
	{/if}
</main>

<style>
    main {
        text-align: center;
        padding: 1em;
        max-width: 240px;
        margin: 0 auto;
    }
</style>
