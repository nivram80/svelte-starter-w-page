<script>
  import { theme } from "./stores.js";
  import Theme from "./Theme.svelte";
  import Radio from "./Radio.svelte";
  import RadioGroup from "./RadioGroup.svelte";
  import Button from "./Button.svelte";
  import Checkbox from "./Checkbox.svelte";
  import Select from "./Select.svelte";
  
  let agreeToTerms = true;
  let arbitraryBoolean = false;
  let arbitraryBooleanII = false;
  let arbitraryBooleanIII = true;
  let automaticallySendEmail = false;
  let font = "Roboto";
  let fontOptions = [
    { id: "1000", fontName: "Helvetica" },
    { id: "1001", fontName: "Helvetica Greek" },
    { id: "1002", fontName: "Times New Roman" },
    { id: "1003", fontName: "Roboto" },
    { id: "1011", fontName: "Comic Sans" },
    { id: "1012", fontName: "Courier" },
    { id: "1024", fontName: "Arial" }
  ];

  const updateTheme = event => {
    theme.update(() => event.target.value);
  };
  const updateAgreeToTerms = event => (agreeToTerms = event.target.checked);
  const updateAutomaticallySendEmail = event =>
    (automaticallySendEmail = event.target.checked);
  const updateArbitraryBoolean = event =>
    (arbitraryBoolean = event.target.checked);
  const updateArbitraryBooleanII = event =>
    (arbitraryBooleanII = event.target.checked);
  const updateArbitraryBooleanIII = event =>
    (arbitraryBooleanIII = event.target.checked);
  const updateFont = event => (font = event.detail);
</script>

<RadioGroup
  label="Choose your theme"
  caption="This will be the colors for your widget.">
  <Radio
    control={$theme}
    name="theme"
    value="default"
    label="Default"
    on:click={updateTheme} />
  <Radio
    control={$theme}
    name="theme"
    value="dark"
    label="Dark"
    on:click={updateTheme} />
  <Radio
    control={$theme}
    name="theme"
    value="merica"
    label="Merica"
    on:click={updateTheme} />
</RadioGroup>

<br />

<Checkbox
  label="I agree to your outragous terms and conditions that I did not read."
  on:click={updateAgreeToTerms}
  name="agreeToTerms"
  checked={agreeToTerms}
  hasError={false} />
<Checkbox
  label="Automatically send me an email"
  on:click={updateAutomaticallySendEmail}
  name="automaticallySendEmail"
  checked={automaticallySendEmail}
  hasError={false} />
<Checkbox
  label="Error checkbox"
  on:click={updateArbitraryBoolean}
  name="arbitraryBoolean"
  checked={arbitraryBoolean}
  hasError />
<Checkbox
  label="Disabled checkbox"
  on:click={updateArbitraryBooleanII}
  name="arbitraryBooleanII"
  checked={arbitraryBooleanII}
  hasError={false}
  disabled />
<Checkbox
  label="Checked Disabled checkbox"
  on:click={updateArbitraryBooleanIII}
  name="arbitraryBooleanIII"
  checked={arbitraryBooleanIII}
  hasError={false}
  disabled />

<br />

<div>Agree to terms: {agreeToTerms}</div>
<div>Automatically Send Email: {automaticallySendEmail}</div>
<div>Arbitrary Boolean: {arbitraryBoolean}</div>
<div>Arbitrary Boolean II: {arbitraryBooleanII}</div>
<div>Arbitrary Boolean III: {arbitraryBooleanIII}</div>

<br />

<Button type="primary">Primary</Button>
<Button type="secondary">Secondary</Button>
<Button type="tertiary">Tertiary</Button>
<Button type="tertiary-danger">Tertiary Danger</Button>
<Button type="primary" disabled>Disabled</Button>

<Theme />

<br />

<Select
  control="fontName"
  key="id"
  label="Choose your font"
  placeholder="Select..."
  initialValue={font}
  options={fontOptions}
  on:inputChanged={event => updateFont(event)} />

<br />
Font: {font}
