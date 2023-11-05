<script>
    import { createEventDispatcher } from 'svelte';
    export let text;
    export let selected = false;
    
    const dispatch = createEventDispatcher();
    
    function toggleSelection() {
      dispatch('toggle', text);
    }
  </script>
  
  
  <style>
    .answer {
      padding: 1rem;
      margin: 0.5rem 0;
      border: 1px solid transparent;
      border-radius: 8px;
      transition: background-color 0.3s, border-color 0.3s;
      cursor: pointer;
    }
  
    .answer:hover {
      background-color: #f0f0f0; /* Slight change on hover */
    }
  
    .answer.selected {
      background-color: #e0e0e0; /* Different color when selected */
      border-color: #d0d0d0;
    }
  </style>
  
  <div class="answer {selected ? 'selected' : ''}" on:click={toggleSelection}>
    {text}
  </div>
  