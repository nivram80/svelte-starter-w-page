<script>
  export let checked = false;
  export let disabled = false;
  export let hasError = false;
  export let label;
  export let name;
</script>

<div class="checkbox-container" class:error={hasError}>
  <input
    type="checkbox"
    id={name}
    {checked}
    {name}
    {disabled}
    on:click />
  <label for={name}>
    <div class="checkbox">
      <div class="checkmark" />
    </div>
    <div class="label-text">{label}</div>
  </label>
</div>

<style>
  input {
    position: absolute;
    opacity: 0;
    margin: 0;
    padding: 0;
  }
  label {
    display: inline-block;
    cursor: pointer;
    margin-right: 20px;
  }
  .label-text {
    display: inline-block;
    padding-left: 1px;
  }
  .checkbox {
    position: relative;
    top: 4px;
    display: inline-block;
    box-sizing: border-box;
    width: 20px;
    height: 20px;
    border: 2px solid var(--rml-gray-tint);
    border-radius: 4px;
    background-color: transparent;
    transition: all 0.25s ease;
  }
  input:checked + label .checkbox {
    background-color: var(--rml-primary-base);
    border-color: var(--rml-primary-base);
  }
  input:hover + label .checkbox,
  input:focus + label .checkbox {
    background-color: var(--rml-gray-shade);
  }
  input:checked:hover + label .checkbox,
  input:checked:focus + label .checkbox {
    background-color: var(--rml-primary-shade);
    border-color: var(--rml-primary-shade);
  }
  input:disabled + label {
    cursor: not-allowed;
  }
  input:disabled + label .checkbox,
  input:disabled:hover + label .checkbox {
    background-color: var(--rml-gray-shade);
    border-color: var(--rml-gray-shade);
  }
  .checkmark {
    position: absolute;
    top: 3px;
    left: 2px;
    display: inline-block;
    width: 10px;
    height: 4px;
    color: transparent;
    border-left: 2px solid;
    border-bottom: 2px solid;
    transform: rotate(-45deg);
  }
  input:checked + label .checkmark {
    color: var(--rml-primary-contrast);
  }
  .error .checkbox {
    border-color: var(--rml-danger-base);
  }
  .error input:checked + label .checkbox {
    background-color: var(--rml-danger-base);
    border-color: var(--rml-danger-base);
  }
  .error input:hover + label .checkbox,
  .error input:focus + label .checkbox {
    background-color: var(--rml-danger-contrast);
  }
  .error input:checked:focus + label .checkbox,
  .error input:checked:hover + label .checkbox {
    background-color: var(--rml-danger-shade2);
    border-color: var(--rml-danger-shade2);
  }
</style>