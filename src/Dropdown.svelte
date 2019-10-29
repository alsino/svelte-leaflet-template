<script>
  import Select from 'svelte-select';
  import { kreise } from './geodata/kreise.js';
  import { selectedArea, selectedAreaID } from './store/store.js';
  const landKreise = kreise.features;

  let items = landKreise.map((item) =>{
    return {
      label: item.properties['NAME_3'],
      value: item.properties['NAME_3'],
      name_2: item.properties['NAME_2'],
      name_1: item.properties['NAME_1'],
      name_0: item.properties['NAME_0'],
      type_3: item.properties['TYPE_3'],
      id_3: item.properties['ID_3'],
      engtype_3: item.properties['ENGTYPE_3'],
      }
  });

  items = items.sort(function(a, b){
    if(a.label < b.label) { return -1; }
    if(a.label > b.label) { return 1; }
    return 0;
})

  let selectedValue = undefined;
  let selectedID;
  let selectedElement;

  function selectArea(){
    // console.log(selectedValue)
    $selectedAreaID = selectedValue['id_3'];

    selectedElement = landKreise.filter((item)=> {
    return item.properties['ID_3'] == $selectedAreaID;
  })[0]
  $selectedArea = selectedElement;
  }

  function clearSelection(){
    console.log("Selection cleared")
    $selectedAreaID = 244;
    $selectedArea = landKreise[0];
  }

</script>

<style>

/* .themed {
    --border: 3px solid blue;
    --borderRadius: 10px;
    --placeholderColor: blue;
  } */

</style>

<div class="themed">
  <Select {items} on:select={selectArea} on:clear={clearSelection} bind:selectedValue ></Select>
</div>


<!-- <div>Select area …</div>
<select name="dropdown" id="dropdown" bind:value={selectedID} on:change= {selectArea}>
	{#each landKreise as lk}
    <option value="{lk.properties['ID_3']}">{lk.properties['NAME_3']}</option>
	{/each}
</select> -->



