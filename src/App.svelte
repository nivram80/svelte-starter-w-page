<script>
  import { Router, Route, Link } from 'svero';
  import StyleGuide from "./StyleGuide.svelte";
  import Settings from "./Settings.svelte";
</script>

<Router>
  <Route path="/" />
  <Route path="/styleGuide" component={StyleGuide} />
  <Route path="/settings" component={Settings} />
</Router>

<Link href="/styleGuide">StyleGuide</Link>
<Link href="/settings">Settings</Link>
