<script>
    export let name = ""; // Exported so it can be bound to a parent component
  
    // Optional: An update event that can be listened to by parent components
    export let onUpdate = (value) => {};
    
    // Handles input changes
    function handleChange(event) {
      const { value } = event.target;
      name = value;
      onUpdate(name); // Emit the updated value
    }
  </script>
  
  <input
    type="text"
    placeholder="Enter your name"
    class="name-input"
    value={name}
    on:input={handleChange}
  />
  
  <style>
    .name-input {
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
  
    .name-input:focus {
      border-color: #0077ff; /* Blue border on focus for better visibility */
      box-shadow: 0 0 0 2px rgba(0, 119, 255, 0.2); /* Glow effect on focus */
    }
  
    .name-input::placeholder {
      color: #aaa; /* Light color for placeholder text */
    }
  </style>
  