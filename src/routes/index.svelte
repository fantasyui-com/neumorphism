
<script>

// import Range from '../components/Range.svelte';




import hljs from 'highlight.js/lib/highlight.js';
import cssLang from 'highlight.js/lib/languages/less';
import htmlLang from 'highlight.js/lib/languages/xml';

hljs.registerLanguage('css', cssLang);
hljs.registerLanguage('html', htmlLang);

let code = `
<div class="neumorphic jumbotron">
  <h1 class="display-4">Hello, world!</h1>
  <p class="lead">This is a simple jumbotron...</p>
  <hr class="my-4">
  <p>It uses utility classes for typography and spacing...</p>
  <a class="btn btn-primary btn-lg" href="." role="button">Learn more</a>
</div>
`;
let example = hljs.highlight('html', code).value.replace(/neumorphic/,'<span class="text-danger">neumorphic</span>')


import chroma from 'chroma-js';



import emotion from 'emotion';
const { css } = emotion;

import sprintfJs from "sprintf-js";
const { sprintf } = sprintfJs;

let display = 'sourcecode';


let colorSaturationFraction = .6;

let lightIntensityRange = [.5,3];
let lightIntensityFraction = .5;
$: lightIntensity = (lightIntensityRange[0] + ((lightIntensityRange[1]-lightIntensityRange[0]) * lightIntensityFraction)).toFixed(1);

let baseColorSelection = '#e0e0e0';
$: baseColor = baseColorSelection;

$: baseColorDark = chroma(baseColorSelection)
  .darken(lightIntensity)
  .saturate(.2*colorSaturationFraction)
  .mix(baseColor ,1-colorSaturationFraction)
  .hex();
$: baseColorLight = chroma(baseColorSelection)
  .brighten(lightIntensity)
  .saturate(.5*colorSaturationFraction)
  .mix(baseColor ,1-colorSaturationFraction)
  .hex();



let borderRadiusRange = [.2,1.5];
let borderRadiusFraction = .2;
$: borderRadius = (borderRadiusRange[0] + ((borderRadiusRange[1]-borderRadiusRange[0]) * borderRadiusFraction)).toFixed(1);

let gradientAngleRange = [0,359];
let gradientAngleFraction = .42;
$: gradientAngle = (gradientAngleRange[0] + ((gradientAngleRange[1]-gradientAngleRange[0]) * gradientAngleFraction)).toFixed(0);






let lightSourceSelection = 0;
$: lightSource = parseInt(lightSourceSelection);

function offsetTransformer(boxShadowOffset, lightSource){

  if(lightSource == 0){
    return [boxShadowOffset,boxShadowOffset,-boxShadowOffset,-boxShadowOffset]
  }else if (lightSource == 1) {
    return [-boxShadowOffset,boxShadowOffset,boxShadowOffset,-boxShadowOffset]
  }else if (lightSource == 2) {
    return [-boxShadowOffset,-boxShadowOffset,boxShadowOffset,boxShadowOffset]
  }else if (lightSource == 3) {
    return [boxShadowOffset,-boxShadowOffset,-boxShadowOffset,boxShadowOffset]
  } else {
    return [boxShadowOffset,boxShadowOffset,boxShadowOffset,boxShadowOffset]
  }

}


let boxShadowOffsetRange = [2,16];
let boxShadowOffsetFraction = .6;
$: boxShadowOffsetValue = (boxShadowOffsetRange[0] + ((boxShadowOffsetRange[1]-boxShadowOffsetRange[0]) * boxShadowOffsetFraction)).toFixed(0);
$: boxShadowOffset = offsetTransformer(boxShadowOffsetValue, lightSource);

let boxShadowBlurRange = [0,32];
let boxShadowBlurFraction = .7;
$: boxShadowBlur = (boxShadowBlurRange[0] + ((boxShadowBlurRange[1]-boxShadowBlurRange[0]) * boxShadowBlurFraction)).toFixed(0);

let boxShadowSpreadRange = [0,16];
let boxShadowSpreadFraction = .2;
$: boxShadowSpread = (boxShadowSpreadRange[0] + ((boxShadowSpreadRange[1]-boxShadowSpreadRange[0]) * boxShadowSpreadFraction)).toFixed(0);







let surfaceModeSelection = 1;
$: surfaceMode = parseInt(surfaceModeSelection);

// NOTE: box-shadow -> offset-x | offset-y | blur-radius | spread-radius | color

$: sourceCode = [
  // Flat
  `
  /* for use on background-color: ${baseColorSelection}; */
  border-radius: ${borderRadius}rem;
  box-shadow: ${boxShadowOffset[0]}px ${boxShadowOffset[1]}px ${boxShadowBlur}px ${boxShadowSpread}px ${baseColorDark}, ${boxShadowOffset[2]}px ${boxShadowOffset[3]}px ${boxShadowBlur}px ${boxShadowSpread}px ${baseColorLight};
  background-color: ${baseColor} ! important;
  `,
  // Concave
  `
  /* for use on background-color: ${baseColorSelection}; */
  border-radius: ${borderRadius}rem;
  box-shadow: ${boxShadowOffset[0]}px ${boxShadowOffset[1]}px ${boxShadowBlur}px ${boxShadowSpread}px ${baseColorDark}, ${boxShadowOffset[2]}px ${boxShadowOffset[3]}px ${boxShadowBlur}px ${boxShadowSpread}px ${baseColorLight};
  background: linear-gradient(${gradientAngle}deg, ${baseColorDark}, ${baseColorLight});
  `,
  // Convex
  `
  /* for use on background-color: ${baseColorSelection}; */
  border-radius: ${borderRadius}rem;
  box-shadow: ${boxShadowOffset[0]}px ${boxShadowOffset[1]}px ${boxShadowBlur}px ${boxShadowSpread}px ${baseColorDark}, ${boxShadowOffset[2]}px ${boxShadowOffset[3]}px ${boxShadowBlur}px ${boxShadowSpread}px ${baseColorLight};
  background: linear-gradient(${gradientAngle}deg, ${baseColorLight}, ${baseColorDark});
  `,
  // Inset
  `
  /* for use on background-color: ${baseColorSelection}; */
  border-radius: ${borderRadius}rem;
  box-shadow: inset ${boxShadowOffset[0]}px ${boxShadowOffset[1]}px ${boxShadowBlur}px ${boxShadowSpread}px ${baseColorDark}, inset ${boxShadowOffset[2]}px ${boxShadowOffset[3]}px ${boxShadowBlur}px ${boxShadowSpread}px ${baseColorLight};
  background: linear-gradient(${gradientAngle}deg, ${baseColorDark}, ${baseColorLight});
  `,
];

$: neumorphic = css`${sourceCode[surfaceMode]}`;


function highlightCss(code){
  return hljs.highlight('css', code).value
}


$: userCode = highlightCss(`
.neumorphic {
${sourceCode[surfaceMode]}
}
`);



</script>

<svelte:head>
  <title>neumorphism</title>
</svelte:head>

<style>



</style>


<div class="container-fluid mb-0" style="min-height: 10rem;">
  <div class="row">
    <div class="col-12 col-md-6 col-lg-9 p-5 shadow" style="background:{baseColor};">

      <h4 class="mb-4">Preview</h4>

      <!-- <div class="{neumorphic} jumbotron">
        <h1 class="display-4">Hello, world!</h1>
        <p class="lead">This is a simple hero unit, a simple jumbotron-style component for calling extra attention to featured content or information.</p>
        <hr class="my-4">
        <p>It uses utility classes for typography and spacing to space content out within the larger container.</p>
        <a class="btn btn-primary btn-lg" href="." role="button">Learn more</a>
      </div> -->


      <div class="{neumorphic} alert alert-success mb-5" role="alert">
        <h4 class="alert-heading">Well done!</h4>
        <p>Aww yeah, you successfully read this important alert message. This example text is going to run a bit longer so that you can see how spacing within an alert works with this kind of content.</p>
        <hr>
        <p class="mb-0">Whenever you need to, be sure to use margin utilities to keep things nice and tidy.</p>
      </div>

      <div class="{neumorphic} alert alert-success mb-5 border-0" role="alert">
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


      <div class="card-deck mt-4">


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



    </div>

    </div>

    <div class="col-12 col-md-6 col-lg-3 p-5 bg-dark text-white shadow">
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
      <label class="small" for="colorSaturation">Color Saturation ({colorSaturationFraction})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">
          <input type="range" class="custom-range" bind:value={colorSaturationFraction} min="0" max="1" step="0.01" id="colorSaturation">
        </div>
      </div>
    </div>

    <div class="card-text">
      <label class="small" for="lightIntensity">Light Intensity ({lightIntensityFraction})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">
          <input type="range" class="custom-range" bind:value={lightIntensityFraction} min="0" max="1" step="0.01" id="lightIntensity">
        </div>
      </div>
    </div>

    <div class="card-text">
      <label class="small" for="surfaceMode">Surface Mode ({surfaceModeSelection})</label>
      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <label class="input-group-text bg-dark text-light" for="surfaceMode">Surface</label>
        </div>
        <select class="custom-select" id="surfaceMode" bind:value={surfaceModeSelection}>
          <option value="0">Flat</option>
          <option selected value="1">Concave</option>
          <option value="2">Convex</option>
          <option value="3">Inset</option>
        </select>
      </div>
    </div>

    <div class="card-text">
      <label class="small" for="lightSource">Light Source ({lightSourceSelection})</label>
      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <label class="input-group-text bg-dark text-light" for="lightSource">Light</label>
        </div>
        <select class="custom-select" id="lightSource" bind:value={lightSourceSelection}>
          <option selected value="0">&nwarr; NW</option>
          <option value="1">&nearr; NE</option>
          <option value="2">&searr; SE</option>
          <option value="3">&swarr; SW</option>
        </select>
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

    <div class="card-text" class:text-muted={surfaceMode=='0'}>
      <label class="small" for="gradientAngle">Gradient Angle ({gradientAngleFraction})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">
          <input type="range" class="custom-range" bind:value={gradientAngleFraction} min="0" max="1" step="0.01" id="gradientAngle" disabled={surfaceMode=='0'} >
        </div>
      </div>
    </div>



    <div class="card-text">
      <label class="small" for="boxShadowOffset">Distance Offset ({boxShadowOffsetFraction})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">
          <input type="range" class="custom-range" bind:value={boxShadowOffsetFraction} min="0" max="1" step="0.01" id="boxShadowOffset">
        </div>
      </div>
    </div>

    <div class="card-text">
      <label class="small" for="boxShadowSpread">Shadow Spread ({boxShadowSpreadFraction})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">
          <input type="range" class="custom-range" bind:value={boxShadowSpreadFraction} min="0" max="1" step="0.01" id="boxShadowSpread">
        </div>
      </div>
    </div>

    <div class="card-text">
      <label class="small" for="boxShadowBlur">Shadow Blur ({boxShadowBlurFraction})</label>
      <div class="input-group mb-3">
        <div class="custom-control custom-range">
          <input type="range" class="custom-range" bind:value={boxShadowBlurFraction} min="0" max="1" step="0.01" id="boxShadowBlur">
        </div>
      </div>
    </div>




    </div>

  </div>
</div>





<p class="small text-muted shadow-sm mb-0 p-3">Place the generated CSS in your application code.</p>

<pre class="mb-0 shadow">
<code class="language-css css hljs">
{@html userCode}
</code>
</pre>

<p class="small text-muted shadow-sm mb-0 p-3">Apply the <span class="text-danger">neumorphic</span> class where needed. Jumbotron, for example: </p>

<pre class="mb-0 shadow">
  <code class="language-html html hljs rounded ">
    {@html example}
  </code>
</pre>


<p class="small text-muted shadow-sm mb-0 p-3">Visit <a href="https://github.com/fantasyui-com/neumorphism" rel="noopener noreferrer" target="_blank">https://github.com/fantasyui-com/neumorphism</a> for more.</p>
