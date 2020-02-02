<script>
  export let segment;












  let measurementFormatter = function(i,min,max){
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

  let measurementInitial = .25;
  let measurementPercentInitial = 50;
  let measurementPercent = measurementPercentInitial;
  let measurementValue = measurementInitial;
  let measurementRange = [0,1];

  let measurementDelta   = 0.05;

  let measurementMinReset     = 0;
  let measurementMaxReset     = 1;


  let measurementMin     = 0-measurementDelta;
  let measurementMax     = 1+measurementDelta;

  let measurementStep    = .01;

  $: measurementStandard = measurementFormatter(measurementValue, measurementMinReset, measurementMaxReset);
  $: measurementSmall   = measurementFormatter(measurementValue - measurementDelta, measurementMinReset, measurementMaxReset);
  $: measurementLarge   = measurementFormatter(measurementValue + measurementDelta, measurementMinReset, measurementMaxReset);





</script>

<style>

</style>

<div class="card-text">
  <label class="small" for="measurement">Border Radius ({measurementStandard})</label>
  <div class="input-group mb-3">
    <div class="custom-control custom-range">
      <input type="range" class="custom-range" bind:value={measurementValue} min="{measurementMin}" max="{measurementMax}" step="{measurementStep}" id="measurement">
    </div>
  </div>
</div>
