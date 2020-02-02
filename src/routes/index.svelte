
<script>

import emotion from 'emotion';
const { css } = emotion;

import sprintfJs from "sprintf-js";
const { sprintf } = sprintfJs;

let display = 'sourcecode';

let px = i => `${i}px`;
let pc = i => `${i}%`;
let rem = i => `${i}rem`.replace(/^0/,'');




let borderRadiusFormatter = function(i,min,max){
  if(i<min) i = min;
  if(i>max) i = max;
  // format number to to a predictable string state
  let response = sprintf('%.2f', i) + 'rem';
  // remove unwanted human based patterns from string
  if(response.match(/^0.00rem$/)) response = '0rem';
  if(response.match(/^1.00rem$/)) response = '1rem';
  if(response.match(/^0\./)) response = response.replace(/^0\./,'.'); // 0.10rem;
  if(response.match(/0+rem$/)) response = response.replace(/0+rem$/,'rem'); // 0.10rem;
  if(response == 'rem') response = '0rem';
  return response;
}

let borderRadiusInitial = .25;
let borderRadiusValue = borderRadiusInitial;
let borderRadiusDelta   = 0.05;

let borderRadiusMinReset     = 0;
let borderRadiusMaxReset     = 1;

let borderRadiusMin     = 0-borderRadiusDelta;
let borderRadiusMax     = 1+borderRadiusDelta;
let borderRadiusStep    = .01;
$: borderRadiusStandard = borderRadiusFormatter(borderRadiusValue, borderRadiusMinReset, borderRadiusMaxReset);
$: borderRadiusSmall   = borderRadiusFormatter(borderRadiusValue - borderRadiusDelta, borderRadiusMinReset, borderRadiusMaxReset);
$: borderRadiusLarge   = borderRadiusFormatter(borderRadiusValue + borderRadiusDelta, borderRadiusMinReset, borderRadiusMaxReset);






const brand = '#74D900';

// LIVE CSS CODE HERE - this CANNOT not used in bootstrap, it is for preview only...
$: btn = css`
  border-radius: ${borderRadiusStandard};
  background: linear-gradient(145deg, #e0eef6, #bcc8cf);
  box-shadow: 6px 6px 12px #adb8bf, -6px -6px 12px #f5ffff;
`;
//(Math.floor(((configuration.borderRadius*.03) / 4) * 100))
$: scssVariables = `

$border-radius:               ${borderRadiusStandard};
$border-radius-sm:            ${borderRadiusSmall};
$border-radius-lg:            ${borderRadiusLarge};

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
      <label class="small" for="borderRadius">Border Radius ({borderRadiusStandard})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">

          <input type="range" class="custom-range" bind:value={borderRadiusValue} min="{borderRadiusMin}" max="{borderRadiusMax}" step="{borderRadiusStep}" id="borderRadius">



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
