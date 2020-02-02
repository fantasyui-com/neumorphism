
<script>

import emotion from 'emotion';
const { css } = emotion;

import sprintfJs from "sprintf-js";
const { sprintf } = sprintfJs;

let display = 'sourcecode';




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
$: neumorphic = css`
  border-radius: ${borderRadiusStandard};
  xbackground: linear-gradient(145deg, #e0eef6, #bcc8cf);
  box-shadow: 6px 6px 12px #adb8bf, -6px -6px 12px #f5ffff;
`;
$: card = css`
  border-radius: ${borderRadiusStandard};
  xbackground: linear-gradient(145deg, #e0eef6, #bcc8cf);
  box-shadow: 6px 6px 12px #adb8bf, -6px -6px 12px #f5ffff;
`;
//(Math.floor(((configuration.borderRadius*.03) / 4) * 100))
$: scssVariables = `

$body-bg:                   $white !default;

$border-radius:               ${borderRadiusStandard};
$border-radius-sm:            ${borderRadiusSmall};
$border-radius-lg:            ${borderRadiusLarge};

$box-shadow-sm:               0 .125rem .25rem rgba($black, .075);
$box-shadow:                  0 .5rem 1rem rgba($black, .15);
$box-shadow-lg:               0 1rem 3rem rgba($black, .175);

$box-shadow-inset:            inset 0 1px 2px rgba($black, .075);

`;

</script>

<svelte:head>
  <title>neumorphism</title>
</svelte:head>

<style>



</style>


<div class="container-fluid" style="min-height: 48rem;">
  <div class="row">
    <div class="col-9 p-5">

      <h4 class="mb-0">Preview</h4>
      <div class="mb-3"><small class="text-muted">Design rich bootstrap components with neumorphic class.</small></div>

      <div class="{neumorphic} jumbotron">
        <h1 class="display-4">Hello, world!</h1>
        <p class="lead">This is a simple hero unit, a simple jumbotron-style component for calling extra attention to featured content or information.</p>
        <hr class="my-4">
        <p>It uses utility classes for typography and spacing to space content out within the larger container.</p>
        <a class="btn btn-primary btn-lg" href="#" role="button">Learn more</a>
      </div>


      <div class="{neumorphic} alert alert-success" role="alert">
        <h4 class="alert-heading">Well done!</h4>
        <p>Aww yeah, you successfully read this important alert message. This example text is going to run a bit longer so that you can see how spacing within an alert works with this kind of content.</p>
        <hr>
        <p class="mb-0">Whenever you need to, be sure to use margin utilities to keep things nice and tidy.</p>
      </div>

      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="neumorphic btn btn-primary {neumorphic}">Primary</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="neumorphic btn btn-secondary {neumorphic}">Secondary</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="neumorphic btn btn-success {neumorphic}">Success</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="neumorphic btn btn-danger {neumorphic}">Danger</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="neumorphic btn btn-warning {neumorphic}">Warning</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="neumorphic btn btn-info {neumorphic}">Info</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="neumorphic btn btn-light {neumorphic}">Light</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="neumorphic btn btn-dark {neumorphic}">Dark</button></div>


      <div class="card-deck">


          <div class="{neumorphic} card text-white bg-primary {card}">
            <div class="card-header">Header</div>
            <div class="card-body">
              <h5 class="card-title">Info card title</h5>
              <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
            </div>
          </div>
          <div class="{neumorphic} card bg-light {card}">
            <div class="card-header">Header</div>
            <div class="card-body">
              <h5 class="card-title">Light card title</h5>
              <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
            </div>
          </div>
          <div class="{neumorphic} card text-white bg-dark {card}">
            <div class="card-header">Header</div>
            <div class="card-body">
              <h5 class="card-title">Dark card title</h5>
              <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
            </div>
          </div>


    </div>

    </div>

    <div class="col-3 p-5">
    <h4 class="mb-0">Neumorphic Settings</h4>
    <div class="mb-3"><small class="text-muted">neumorphic class configuration</small></div>

    <div class="card-text">
      <label class="small" for="borderRadius">Border Radius ({borderRadiusStandard})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">
          <input type="range" class="custom-range" bind:value={borderRadiusValue} min="{borderRadiusMin}" max="{borderRadiusMax}" step="{borderRadiusStep}" id="borderRadius">
        </div>
      </div>
    </div>

    <h4 class="mb-0 mt-5">Custom Settings</h4>
    <div class="mb-3"><small class="text-muted">Settings for custom utility classes.</small></div>


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
