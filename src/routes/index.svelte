
<script>

import emotion from 'emotion';
const { css } = emotion;


let display = 'sourcecode';

const configuration = {
  borderRadius: '48px'
};





const brand = '#74D900';

$: btn = css`
  border-radius: ${configuration.borderRadius};
  background: linear-gradient(145deg, #e0eef6, #bcc8cf);
  box-shadow: 6px 6px 12px #adb8bf, -6px -6px 12px #f5ffff;
`;

</script>

<svelte:head>
  <title>neumorphism</title>
</svelte:head>

<style>



</style>


<div class="container-fluid" style="min-height: 48rem;">
  <div class="row">
    <div class="col p-5">

      <h6>Button Preview</h6>
      <p>Configure your design, and click generate</p>

      <button type="button" class="btn btn-primary {btn}">Primary</button>
      <button type="button" class="btn btn-secondary {btn}">Secondary</button>
      <button type="button" class="btn btn-success {btn}">Success</button>
      <button type="button" class="btn btn-danger {btn}">Danger</button>
      <button type="button" class="btn btn-warning {btn}">Warning</button>
      <button type="button" class="btn btn-info {btn}">Info</button>
      <button type="button" class="btn btn-light {btn}">Light</button>
      <button type="button" class="btn btn-dark {btn}">Dark</button>
      <button type="button" class="btn btn-link {btn}">Link</button>

    </div>

    <div class="col p-5">
      One of three columns
    </div>

  </div>
</div>


<nav>
  <ul class="nav nav-tabs">
    <li class="nav-item">
      <a class:active='{display === "sourcecode"}' class="nav-link" on:click={()=>display='sourcecode'}>Sourcecode</a>
    </li>
    <li class="nav-item">
      <a class:active='{display === "debugger"}' class="nav-link" on:click={()=>display='debugger'}>Debugger</a>
    </li>
  </ul>
</nav>
