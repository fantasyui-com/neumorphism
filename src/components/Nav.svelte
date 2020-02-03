<script>
  export let segment;
</script>

<style>

</style>

<nav class="bg-dark shadow">
  <ul class="nav nav-tabs">

    <li class="nav-item">
      <a class:active='{segment === undefined}' class="nav-link" href=".">Neumorphism</a>
    </li>

    <li class="nav-item">
      <a class:active='{segment === "help"}' class="nav-link" href="help">Help</a>
    </li>

  </ul>
</nav>
