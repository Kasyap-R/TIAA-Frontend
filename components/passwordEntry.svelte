<script>
    import { createEventDispatcher } from 'svelte';
  
    let password = ""; // Local variable within the component
    const dispatch = createEventDispatcher();
  
    // Dispatches the 'update' event with the current value of the password
    function handleChange(event) {
      password = event.target.value;
      dispatch('update', { password });
    }
  </script>
  
  <input
    type="password"
    placeholder="Enter your password"
    class="password-input"
    value={password}
    on:input={handleChange}
  />
  
  <style>
    .password-input {
      padding: 10px;
      font-size: 1rem;
      border: 1px solid #ccc; /* Light grey border */
      border-radius: 5px;
      outline: none;
      width: 100%; /* Full width */
      max-width: 400px; /* Maximum width so it doesn't get too long */
      box-sizing: border-box; /* Ensures padding does not affect the overall width */
      margin-bottom: 10px; /* Space below the input */
    }
  
    .password-input:focus {
      border-color: #0077ff; /* Blue border on focus for better visibility */
      box-shadow: 0 0 0 2px rgba(0, 119, 255, 0.2); /* Glow effect on focus */
    }
  
    .password-input::placeholder {
      color: #aaa; /* Light color for placeholder text */
    }
  </style>
  