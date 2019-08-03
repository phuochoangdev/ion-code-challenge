<template>
  <div :style="{width: '800px', margin: '0 auto'}">
    <div class="row mb-1">
      <p class="col-sm-8">Render a dynamic form.</p>
      <p>More detailed in <strong>readme.md</strong> file</p>
    </div>
    <!--Your code goes here!-->
  </div>
</template>

<script>
/********
 * Render a form with the following requirements:
    - Use data from this end point localhost:8080/structure as the structure of this form. Keep in mind that this structure can be changed dynamically.
    - Use data from this end point localhost:8080/data as initial data.
    - Add validation (for fields those marked 'required' in structure)
 * API explaination:
  -
*******/
export default {
}
</script>

<style scoped>
  * {
    -webkit-font-smoothing: antialiased;
  }
  *, :after, :before {
    box-sizing: border-box;
  }

</style>
