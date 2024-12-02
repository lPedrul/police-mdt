<script>
  import { Button, Input, Label } from 'flowbite-svelte';
  import { AngleRightOutline, SearchOutline } from 'flowbite-svelte-icons';
</script>

<div class="flex flex-rol h-full max-h-full justify-between">
  <button
    class="shrink flex bg-gray-700 pt-1 mr-1 text-center h-full items-center"
  >
    <p class=" font-bold"><AngleRightOutline /></p>
  </button>
  <div class="grow flex flex-col bg-gray-700 px-2 pt-1 mr-1">
    <h1 class="font-bold mb-1">Incidents</h1>
    <div class="self-center w-full">
      <Input
        type="text"
        id="search-input-incidents"
        class="h-full bg-slate-600 w-full border-slate-500 text-slate-400 py-[0.2rem] pl-6"
        placeholder="Search"
      >
        <SearchOutline
          slot="left"
          class="w-4 h-4 ml-1 text-slate-300 relative top-[0.45rem]"
        />
      </Input>
    </div>
    <hr class="w-full self-center border-t-slate-500 mt-2 mb-1" />
    <div class="self-center w-full">
      <div class="my-1 bg-slate-800 flex justify-between px-1">
        <div class="">
          <p>Henry Armstrong - Street Race</p>
          <p>ID: 000001</p>
        </div>
        <div class="">
          <p class=" text-right">5 Hours Ago</p>
          <p class=" text-right">Phillip Collins</p>
        </div>
      </div>
      <div class="my-1 bg-slate-800">tudo bem</div>
      <div class="my-1 bg-slate-800">e vc</div>
    </div>
  </div>
  <div class="grow bg-gray-700 mx-1">
    <h1>Editor</h1>
    <div></div>
  </div>
  <div class="bg-gray-700 ml-1">
    <h1>Other stuff</h1>
    <div></div>
  </div>
</div>
