<script>
  export let disabled = false;
  export let size = "regular";
  export let type = "primary";
</script>

<button
  class={`button ${type} ${size}`}
  disabled={disabled}
>
  <slot />
</button>

<style>
  button {
    -webkit-appearance: none;
    padding: 8px 16px;
    font-size: 12px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    outline: none;
    transition: all 0.25s ease;
  }

  .regular {
    height: 32px;
  }

  .primary {
    background-color: var(--rml-primary-base);
    color: var(--rml-primary-contrast);
  }

  .primary:hover:not(:disabled) {
    background-color: var(--rml-primary-shade);  
  }

  .primary:active:not(:disabled),
  .primary:focus:not(:disabled) {
    background-color: var(--rml-primary-tint);  
  }

  .secondary {
    background-color: var(--rml-secondary-base);
    color: var(--rml-secondary-contrast);
  }

  .secondary:hover:not(:disabled) {
    background-color: var(--rml-secondary-shade);  
  }

  .secondary:active:not(:disabled),
  .secondary:focus:not(:disabled) {
    background-color: var(--rml-secondary-tint);  
  }

  .tertiary {
    background-color: var(--rml-tertiary-base);
    color: var(--rml-tertiary-contrast);
  }

  .tertiary:hover:not(:disabled) {
    background-color: var(--rml-tertiary-shade);  
  }

  .tertiary:active:not(:disabled),
  .tertiary:focus:not(:disabled) {
    background-color: var(--rml-tertiary-tint);  
  }

  .tertiary-danger {
    background-color: var(--rml-tertiary-base);
    color: var(--rml-danger-base);
  }

  .tertiary-danger:hover:not(:disabled) {
    background-color: var(--rml-danger-contrast);  
  }

  .tertiary-danger:active:not(:disabled),
  .tertiary-danger:focus:not(:disabled) {
    background-color: var(--rml-danger-tint);  
  }

  .large {
    height: 40px;
    font-size: 16px;
  }

  button:disabled {
    background-color: var(--rml-gray-base);
    color: var(--rml-gray-tint);
    cursor: not-allowed;
  }
</style>