<script>
  import Dropdown from './Dropdown.svelte';
  import { kreise } from './geodata/kreise.js';
  import { selectedAreaID, selectedArea } from './store/store.js';
  const landKreise = kreise.features;

</script>

<style>
  .sidebar {
    flex: 1;
    background: whitesmoke;
  }
</style>

<div class="sidebar">
  <Dropdown/>
  <div>{$selectedAreaID}</div>
  <div>{$selectedArea.properties['NAME_3']}</div>
  <div>{$selectedArea.properties['NAME_2']}</div>
  <div>{$selectedArea.properties['NAME_1']}</div>
  <div>{$selectedArea.properties['NAME_0']}</div>
  <div>{$selectedArea.properties['TYPE_3']}</div>
  <div>{$selectedArea.properties['ENGTYPE_3']}</div>
</div>