<script>
  import { onMount, createEventDispatcher } from "svelte";

  const inputChanged = createEventDispatcher();

  export let control;
  export let disabled = true;
  export let initialValue;
  export let key;
  export let label;
  export let options;
  export let placeholder;

  let filteredOptions = [];
  let isFocused = false;
  let selectedOptionIndex = 0;
  let showOptions = false;
  let value;

  onMount(() => {
    value = initialValue;
    filteredOptions = options;
  });

  const changeValue = option => {
    value = option[control];
    showOptions = false;
    inputChanged("inputChanged", value);
  };
  const filterOptions = value => {
    return options.filter(option =>
      option[control].toLowerCase().includes(value.toLowerCase())
    );
  };
  const isFirstOption = () => selectedOptionIndex === 0;
  const isLastOption = () => selectedOptionIndex === filteredOptions.length - 1;
  const onBlur = () => (isFocused = false);
  const onFocus = () => (isFocused = true);
  const onHover = index => (selectedOptionIndex = index);
  const onInput = event => {
    value = event.target.value;
    filteredOptions = filterOptions(value);
    selectedOptionIndex = 0;
  };
  const onKeyDown = event => {
    if (disabled) return;
    switch (event.key) {
      case "Backspace":
        if (!showOptions) {
          showOptions = true;
        }
        filteredOptions = filterOptions(value);
        break;
      case "Tab":
        (isFocused = false), (showOptions = false);
        break;
      case "Enter":
        event.preventDefault();
        event.stopPropagation();
        if (showOptions) {
          value = filteredOptions[selectedOptionIndex][control];
          showOptions = false;
          inputChanged("inputChanged", value);
        } else {
          showOptions = true;
        }
        break;
      case "Escape":
        event.preventDefault();
        if (showOptions) {
          showOptions = false;
          event.stopPropagation();
        }
        break;
      case " ":
        if (!showOptions) {
          event.preventDefault();
          showOptions = true;
        }
        break;
      case "PageUp":
      case "PageDown":
      case "End":
      case "Home":
        event.preventDefault();
        if (!showOptions) {
          showOptions = true;
        }
        break;
      case "ArrowUp":
        if (showOptions && !isFirstOption()) {
          selectedOptionIndex -= 1;
        } else {
          showOptions = true;
        }
        break;
      case "ArrowDown":
        if (showOptions && !isLastOption()) {
          selectedOptionIndex += 1;
        } else {
          showOptions = true;
        }
        break;
    }
  };
  const toggleOptions = () => {
    if (!disabled) {
      showOptions = !showOptions;
    }
  };
</script>

<style>
  .select-container {
    position: relative;
  }

  label {
    display: inline-block;
    margin-bottom: 8px;
    font-size: 14px;
  }

  .select {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    box-sizing: border-box;
    border: 1px solid var(--rml-gray-base);
    border-radius: 4px;
    background-color: var(--rml-gray-base);
  }

  .select.focused {
    border: 1px solid var(--rml-primary-base);
    background-color: var(--rml-gray-contrast);
    box-shadow: var(--rml-secondary-base) 0 2px 6px;
  }

  .select.disabled {
    border-color: var(--rml-gray-shade);
    background-color: var(--rml-gray-shade);
  }

  .select.disabled input {
    color: var(--rml-gray-base);
  }

  input {
    -webkit-appearance: none;
    box-sizing: border-box;
    width: 100%;
    height: 32px;
    margin: 0;
    padding: 4px 11px;
    border-style: none;
    outline: none;
    border-radius: 4px;
    color: var(--rml-background-contrast);
    font-size: 14px;
    background-color: transparent;
    caret-color: var(--rml-primary-base);
  }

  input:disabled {
    cursor: not-allowed;
  }

  .select-arrow {
    padding-right: 16px;
    cursor: pointer;
  }

  .options {
    position: absolute;
    width: 100%;
    margin: 8px 0 0 0;
    padding: 8px 0;
    border-radius: 8px;
    background-color: var(--rml-background-base);
    box-shadow: rgba(0, 0, 0, 0.16) 0px 2px 6px;
    z-index: 2;
  }

  .option {
    box-sizing: border-box;
    height: 34px;
    padding: 8px 16px;
    list-style-type: none;
    color: var(--rml-gray-tint);
    font-size: 14px;
    font-weight: normal;
    cursor: pointer;
  }

  .option.selected {
    font-weight: bold;
  }

  .option[aria-selected="true"] {
    background-color: var(--rml-gray-base);
    color: var(--rml-default-contrast);
  }
</style>

<div class="select-container">
  <label>{label}</label>
  <div
    aria-haspopup="true"
    aria-expanded={showOptions.toString()}
    aria-controls={showOptions ? control : false}
    class="select"
    class:focused={isFocused}
    class:disabled
    on:click={toggleOptions}
    on:keydown={onKeyDown}>
    <input
      aria-haspopup="true"
      aria-expanded={showOptions.toString()}
      role="combobox"
      type="text"
      {placeholder}
      {value}
      {disabled}
      on:input={onInput}
      on:focus={onFocus}
      on:blur={onBlur} />
    <!-- TODO: Use a proper SVG after we decide what method we'll use to render the SVG (i.e. component, API, CDN?). -->
    <div class="select-arrow">▿</div>
  </div>
  {#if showOptions}
    <ul role="listbox" tabindex="0" class="options" id={control}>
      {#each filteredOptions as option, index}
        <li
          role="option"
          aria-selected={(index === selectedOptionIndex).toString()}
          class="option"
          class:selected={option[control] === value}
          key={option[key]}
          on:click={() => changeValue(option)}
          on:mouseover={() => onHover(index)}>
           {option[control]}
        </li>
      {/each}
    </ul>
  {/if}
</div>
