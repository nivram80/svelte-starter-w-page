<script>
  import StyleGuide from "./StyleGuide.svelte";
  import Settings from "./Settings.svelte";

  let showHome = true;
  let showSettings = false;
  let showStyleGuide = false;

  function goToSettings(ctx, next) {
    showHome = false;
    showStyleGuide = false;
    showSettings = true;
  }

  function goToStyleGuide() {
    showHome = false;
    showSettings = false;
    showStyleGuide = true;
  }

  function goToHome() {
    showSettings = false;
    showStyleGuide = false;
    showHome = true;
  }
</script>

<a href="./">Home</a>
<a href="./styleGuide">StyleGuide</a>
<a href="./settings">Settings</a>

<div id="content"></div>

{#if showSettings}
  <Settings />
{/if}

{#if showStyleGuide}
  <StyleGuide />
{/if}

{#if showHome}
  <div>
    <h1>This is the Home Page!</h1>
  </div>
{/if}