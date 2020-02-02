
<script>

// import Range from '../components/Range.svelte';


import chroma from 'chroma-js';
console.log(chroma);


import emotion from 'emotion';
const { css } = emotion;

import sprintfJs from "sprintf-js";
const { sprintf } = sprintfJs;

let display = 'sourcecode';

let baseColorSelection = '#93a1a1';
$: baseColor = baseColorSelection;
$: baseColorLight = chroma(baseColorSelection).brighten(.8).hex();;
$: baseColorDark = chroma(baseColorSelection).darken().hex();;

let borderRadiusRange = [.2,1.5];
let borderRadiusFraction = .2;
$: borderRadius = (borderRadiusRange[0] + ((borderRadiusRange[1]-borderRadiusRange[0]) * borderRadiusFraction)).toFixed(1);

let gradientAngleRange = [0,359];
let gradientAngleFraction = .42;
$: gradientAngle = (gradientAngleRange[0] + ((gradientAngleRange[1]-gradientAngleRange[0]) * gradientAngleFraction)).toFixed(0);

let neumorphicDistanceRange = [2,16 ];
let neumorphicDistanceFraction = .25;
$: neumorphicDistanceOffset = (neumorphicDistanceRange[0] + ((neumorphicDistanceRange[1]-neumorphicDistanceRange[0]) * neumorphicDistanceFraction)).toFixed(0);
$: neumorphicDistanceBlur = (neumorphicDistanceOffset*1.5).toFixed(0);
$: neumorphicDistanceSpread = (neumorphicDistanceOffset*.5).toFixed(0);

// NOTE: box-shadow -> offset-x | offset-y | blur-radius | spread-radius | color

$: sourceCode = `
  border-radius: ${borderRadius}rem;
  background: linear-gradient(${gradientAngle}deg, ${baseColorDark}, ${baseColorLight});
  box-shadow: ${neumorphicDistanceOffset}px ${neumorphicDistanceOffset}px ${neumorphicDistanceBlur}px ${neumorphicDistanceSpread}px ${baseColorDark}, -${neumorphicDistanceOffset}px -${neumorphicDistanceOffset}px ${neumorphicDistanceBlur}px ${neumorphicDistanceSpread}px ${baseColorLight};
`;

$: neumorphic = css`${sourceCode}`;

$: userCode = `
.neumorphic {
${sourceCode}
}
`;



</script>

<svelte:head>
  <title>neumorphism</title>
</svelte:head>

<style>



</style>


<div class="container-fluid" style="min-height: 48rem;">
  <div class="row">
    <div class="col-9 p-5" style="background:{baseColor};">

      <h4 class="mb-0">Preview</h4>
      <div class="mb-3"><small class="text-muted">Design rich bootstrap components with neumorphic class.</small></div>

      <!-- <div class="{neumorphic} jumbotron">
        <h1 class="display-4">Hello, world!</h1>
        <p class="lead">This is a simple hero unit, a simple jumbotron-style component for calling extra attention to featured content or information.</p>
        <hr class="my-4">
        <p>It uses utility classes for typography and spacing to space content out within the larger container.</p>
        <a class="btn btn-primary btn-lg" href="." role="button">Learn more</a>
      </div> -->


      <div class="{neumorphic} alert alert-success" role="alert">
        <h4 class="alert-heading">Well done!</h4>
        <p>Aww yeah, you successfully read this important alert message. This example text is going to run a bit longer so that you can see how spacing within an alert works with this kind of content.</p>
        <hr>
        <p class="mb-0">Whenever you need to, be sure to use margin utilities to keep things nice and tidy.</p>
      </div>

      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="{neumorphic} btn btn-primary">Primary</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="{neumorphic} btn btn-secondary">Secondary</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="{neumorphic} btn btn-success">Success</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="{neumorphic} btn btn-danger">Danger</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="{neumorphic} btn btn-warning">Warning</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="{neumorphic} btn btn-info">Info</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="{neumorphic} btn btn-light">Light</button></div>
      <div class="pr-3 pb-3 d-inline-block"><button type="button" class="{neumorphic} btn btn-dark">Dark</button></div>


      <div class="card-deck">


          <div class="{neumorphic} card text-white bg-primary">
            <div class="card-header">Header</div>
            <div class="card-body">
              <h5 class="card-title">Info card title</h5>
              <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
            </div>
          </div>
          <div class="{neumorphic} card bg-light">
            <div class="card-header">Header</div>
            <div class="card-body">
              <h5 class="card-title">Light card title</h5>
              <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
            </div>
          </div>
          <div class="{neumorphic} card text-white bg-dark">
            <div class="card-header">Header</div>
            <div class="card-body">
              <h5 class="card-title">Dark card title</h5>
              <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
            </div>
          </div>


    </div>

    </div>

    <div class="col-3 p-5 bg-dark text-white">
    <h4 class="mb-0">Neumorphic Settings</h4>
    <div class="mb-3"><small class="text-muted">neumorphic class configuration</small></div>


    <div class="card-text">
      <label class="small" for="baseColor">Base Color ({baseColorSelection})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">
          <input type="color" bind:value={baseColorSelection} id="baseColor">
        </div>
      </div>
    </div>


    <div class="card-text">
      <label class="small" for="borderRadius">Border Radius ({borderRadiusFraction})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">
          <input type="range" class="custom-range" bind:value={borderRadiusFraction} min="0" max="1" step="0.01" id="borderRadius">
        </div>
      </div>
    </div>

    <div class="card-text">
      <label class="small" for="gradientAngle">Gradient Angle ({gradientAngleFraction})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">
          <input type="range" class="custom-range" bind:value={gradientAngleFraction} min="0" max="1" step="0.01" id="gradientAngle">
        </div>
      </div>
    </div>

    <div class="card-text">
      <label class="small" for="neumorphicDistance">Neumorphic Distance ({neumorphicDistanceFraction})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">
          <input type="range" class="custom-range" bind:value={neumorphicDistanceFraction} min="0" max="1" step="0.01" id="neumorphicDistance">
        </div>
      </div>
    </div>


    </div>

  </div>
</div>


<nav>
  <ul class="nav nav-tabs">
    <li class="nav-item">
      <button class:active='{display === "sourcecode"}' class="nav-link" on:click={()=>display='sourcecode'}>Sourcecode</button>
    </li>
    <li class="nav-item">
      <button class:active='{display === "debugger"}' class="nav-link" on:click={()=>display='debugger'}>Debugger</button>
    </li>
  </ul>
</nav>


<pre>
<code>
{userCode}
</code>
</pre>
