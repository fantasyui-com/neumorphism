
<script>

import emotion from 'emotion';
const { css } = emotion;


let display = 'sourcecode';

let px = i => `${i}px`;
let pc = i => `${i}%`;
let rem = i => `${i}rem`;

const configuration = {
  borderRadius: .25,
};



const brand = '#74D900';

// LIVE CSS CODE HERE - this CANNOT not used in bootstrap, it is for preview only...
$: btn = css`
  border-radius: ${rem(configuration.borderRadius)};
  background: linear-gradient(145deg, #e0eef6, #bcc8cf);
  box-shadow: 6px 6px 12px #adb8bf, -6px -6px 12px #f5ffff;
`;
//(Math.floor(((configuration.borderRadius*.03) / 4) * 100))
$: scssVariables = `

$border-radius-sm:            ${rem(configuration.borderRadius - 0.05  )};
$border-radius:               ${rem(configuration.borderRadius)};
$border-radius-lg:            ${rem(configuration.borderRadius + 0.05 )};

`;

</script>

<svelte:head>
  <title>neumorphism</title>
</svelte:head>

<style>



</style>


<div class="container-fluid" style="min-height: 48rem;">
  <div class="row">
    <div class="col-8 p-5">

      <h4 class="mb-3">Preview</h4>

      <h6>Buttons</h6>
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

    <div class="col-4 p-5">
    <h4 class="mb-3">Settings</h4>

    <div class="card-text">
      <label class="small" for="borderRadius">Border Radius</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">

          <input type="range" class="custom-range" bind:value={configuration.borderRadius} min="0" max="1" step="0.01" id="borderRadius">

        </div>
      </div>
    </div>

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


<pre>
<code>
{scssVariables}
</code>
</pre>
