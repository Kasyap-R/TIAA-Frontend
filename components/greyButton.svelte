<script>
    // This is a placeholder for the click event that can be customized when the button is used
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();
    function handleClick() {
        dispatch("click");
    }
</script>

<button on:click={handleClick} class="btn">
    <slot />
    <!-- This allows for custom button text -->
</button>

<style>
    .btn {
        padding: 0.5em 1em;
        border: none;
        background-color: #757575; /* A shade of grey */
        color: white;
        font-size: 1rem;
        font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
        border-radius: 4px;
        cursor: pointer;
        transition: background-color 0.3s ease;
        outline: none;
    }

    .btn:hover {
        background-color: #5a5a5a; /* A darker shade of grey for hover state */
    }

    .btn:active {
        background-color: #484848; /* An even darker shade for active state */
    }

    .btn:focus {
        box-shadow: 0 0 0 2px rgba(117, 117, 117, 0.4); /* A subtle focus ring */
    }
</style>
