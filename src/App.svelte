<script>
  import { Router, Link, Route } from "svelte-routing";
  import StyleGuide from "./StyleGuide.svelte";
  import Settings from "./Settings.svelte";
</script>

<Router>
  <nav>
    <Link to="/">Home</Link>
    <Link to="styleGuide">StyleGuide</Link>
    <Link to="settings">Settings</Link>
  </nav>
  <div>
    <Route path="styleGuide" component="{StyleGuide}" />
    <Route path="settings" component="{Settings}" />
  </div>
</Router>
