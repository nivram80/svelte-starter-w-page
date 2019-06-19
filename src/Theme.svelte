<script>
  import { theme } from "./stores.js";
</script>

<div class={`theme-section ${$theme}`}>
  {$theme.toUpperCase()}
</div>

<style>
  .theme-section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: 30px;
    border: 20px solid #000;
    width: 280px;
    height: 300px;
    color: var(--rml-primary-contrast);
    font-size: 30px;
  }

  .default {
    background-color: var(--rml-primary-base);
    border-color: var(--rml-background-contrast);
  }

  .dark {
    background-color: #717171;
    border-color: black;
  }

  .merica {
    background-color: red;
    border-color: blue;
  }
</style>