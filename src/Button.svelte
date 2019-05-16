<style>
  button {
    font: inherit;
    padding: 0.15rem 0.5rem;
    background: #d10057;
    border: 1px solid #d10057;
    color: white;
    transition: 0.1s ease-in-out;
    cursor: pointer;
  }
  button:hover,
  button:active {
    background: white;
    color: #d10057;
  }
</style>

<button on:click>
  <slot />
</button>
