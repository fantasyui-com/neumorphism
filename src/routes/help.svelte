<svelte:head>
  <title>Neumorphism Help</title>
</svelte:head>


<script>

import hljs from 'highlight.js/lib/highlight.js';
import html from 'highlight.js/lib/languages/xml';
hljs.registerLanguage('html', html);

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


</script>


<div class="container-fluid text-white" style="min-height: 48rem;">
  <div class="row">
    <div class="col p-5">

    <p class="small">Place the generated CSS in your code and then apply the <span class="text-danger">neumorphic</span> class as needed.</p>

    <pre class="mb-0 shadow-lg">
      <code class="language-html html hljs rounded ">
        {@html example}
      </code>
    </pre>

    </div>
  </div>
  <div class="row">
    <div class="col pl-5">

    See <a href="https://github.com/fantasyui-com/neumorphism" rel="noopener noreferrer" target="_blank">https://github.com/fantasyui-com/neumorphism</a> for more.

    </div>
  </div>
</div>
