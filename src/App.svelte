<script>
  import page from "../node_modules/page";
  import StyleGuide from "./StyleGuide.svelte";
  import Settings from "./Settings.svelte";

  let showHome = true;
  let showSettings = false;
  let showStyleGuide = false;

  page('/', goToHome);
  page('/styleGuide', goToStyleGuide);
  page('/settings', goToSettings);
  page();

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