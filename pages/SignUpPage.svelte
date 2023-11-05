<script>
    import NameEntry from "../components/nameEntry.svelte";
    import PasswordEntry from "../components/passwordEntry.svelte";
    import GreyButton from "../components/greyButton.svelte";
    import {registrationState} from "../stores/store"
    import { createEventDispatcher } from 'svelte'

    const dispatch = createEventDispatcher();

    const API_ENDPOINT = "http://54.210.73.216:"

    let name = '';
    let password = '';

    // Event handlers that update local state
    function handleNameUpdate(event) {
        name = event.detail.name;
    }

    function handlePasswordUpdate(event) {
        password = event.detail.password;
    }

    async function doesUserExist(username) {
        try {
            const response = await fetch(`${API_ENDPOINT}7060/retrieve_user_data/${encodeURIComponent(username)}`);
            console.log(`${API_ENDPOINT}7060/retrieve_user_data/${encodeURIComponent(username)}`)
            if (response.status === 200) {
                // If the response is okay, then the user exists
                
                return true;
            } else if (response.status === 404) {
                // If the response is a 404, then the user does not exist
                return false;
            } else {
                // If another error occurs, log it and treat as if the user does not exist
                console.error('Server error:', response.status);
                return false;
            }
        } catch (error) {
            // If a network error occurs, log it and treat as if the user does not exist
            console.error('Network error:', error);
            return false;
        }
    }

    async function handleSignIn() {
        console.log('Signing in with:', name, password);
        // Check if user exists
        const userExists = await doesUserExist(name);
        
        if (!userExists) {
            alert("Username does not exist!");
            return;
        }

        // Continue with sign-in process
        dispatch('finish', {name: name, new: false});
        registrationState.update(state => ({...state, showDashboard: true, showSignUpPage: false}));
    }

    async function handleSignUp() {
        console.log('Signing up with:', name, password);
        const userExists = await doesUserExist(name);
        if(userExists) {
            alert("Username is already taken!")
            return;
        }
        dispatch('finish', {name: name, new: true});
        registrationState.update(state => ({...state, showPersonalityQuiz: true, showSignUpPage: false}))
    }

</script>


<body>
    <NameEntry on:update={handleNameUpdate}/>
    <PasswordEntry on:update={handlePasswordUpdate}/>
    <GreyButton on:click={handleSignIn}>Sign In</GreyButton>
    <GreyButton on:click={handleSignUp}>Sign Up</GreyButton>
</body>
  


<style>

</style>