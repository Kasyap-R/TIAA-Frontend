<script>
    import SignUpPage from "../pages/SignUpPage.svelte";
	import {registrationState} from "../stores/store";
	import PersonalityQuiz from "../pages/PersonalityQuizContainer.svelte";
	import Dashboard from "../pages/Dashboard.svelte";
	import AvatarCreation from "../pages/AvatarCreation.svelte";

	let resultsString = '';
	let avatarURL = '';
	let username = '';

	function handleQuizFinish(event) {
		const resultsString = event.detail.results;
		console.log('Received quiz results:', resultsString);
	}

	function handleSignUpFinish(event) {
		console.log("User name is")
	}

	async function handleAvatarCreationFinish(event) {
		if(event.detail.new) {
			avatarURL = event.detail.url;
			console.log(avatarURL)
			// Make request to register user, you have all the neccesary data
			
		}
		
		registrationState.update(state => ({...state, showAvatarCreation: false, showDashboard: true}))
	}

	async function registerUser(username, personality_data, avatar_url){

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
