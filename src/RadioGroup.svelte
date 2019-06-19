<script>
  export let caption;
  export let inline = false;
  export let label;
</script>

<div class="radio-group" class:inline>
  <label>{label}</label>
  <div class="radios">
    <slot />
  </div>
  {#if caption}
    <div class="caption">{caption}</div>
  {/if}
</div>

<style>
  label {
    margin-bottom: 3px;
  }
  .inline .radios{
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
  }
  .caption {
    margin-top: 8px;
    font-size: 12px;
  }
</style>