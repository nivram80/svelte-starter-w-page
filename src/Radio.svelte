<script>
  export let control;
  export let disabled = false;
  export let hasError = false;
  export let label;
  export let name;
  export let value;
</script>

<div class="radio-container" class:error={hasError}>
  <input
    type="radio"
    id={value}
    {name}
    {value}
    {disabled}
    checked={control === value}
    on:click />
  <label for={value}>
    <div class="radio">
      <div class="radio-dot" />
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
  .radio {
    position: relative;
    top: 4px;
    display: inline-block;
    box-sizing: border-box;
    width: 20px;
    height: 20px;
    border: 2px solid var(--rml-gray-tint);
    border-radius: 50%;
  }
  input:checked + label .radio {
    background-color: var(--rml-primary-base);
    border-color: var(--rml-primary-base);
  }
  input:hover + label .radio {
    background-color: var(--rml-gray-shade);
  }
  input:focus + label .radio,
  input:checked:hover + label .radio {
    background-color: var(--rml-primary-shade);
    border-color: var(--rml-primary-shade);
  }
  .radio-dot {
    position: absolute;
    top: 5px;
    left: 5px;
    display: inline-block;
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background-color: transparent;
  }
  input:checked + label .radio-dot {
    background-color: var(--rml-primary-contrast);
  }
  .error .radio {
    border-color: var(--rml-danger-base);
  }
  .error input:checked + label .radio {
    background-color: var(--rml-danger-base);
    border-color: var(--rml-danger-base);
  }
  .error input:hover + label .radio {
    background-color: var(--rml-danger-contrast);
  }
  .error input:focus + label .radio,
  .error input:checked:hover + label .radio {
    background-color: var(--rml-danger-shade2);
    border-color: var(--rml-danger-shade2);
  }
</style>