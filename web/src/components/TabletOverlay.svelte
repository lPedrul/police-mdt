<script lang="ts">
  import { Receive } from '@enums/events';
  import { ReceiveEvent } from '@utils/eventsHandlers';

  let size: number = 40;
  let colInvert: boolean = true;
  let text: string = 'Byte Labs';

  ReceiveEvent(Receive.imageResize, (value: number) => {
    size = value;
  });

  ReceiveEvent(Receive.imageInvert, (bool: boolean) => {
    colInvert = bool;
  });

  ReceiveEvent(Receive.changeText, (newtext: string) => {
    text = newtext;
  });

  ReceiveEvent(Receive.resetText, () => {
    text = 'Byte Labs';
  });

  let transparent = false;
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<!-- TODO - colocar true em cima -->
<div
  on:mouseleave={() => (transparent = false)}
  on:mouseenter={() => (transparent = false)}
  class="w-screen h-screen absolute top-0 left-0"
>
  <div
    on:mouseleave={() => (transparent = false)}
    on:mouseenter={() => (transparent = false)}
    class={`
      absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 mx-auto border-zinc-950 border-[14px] rounded-[2.5rem] h-[93vh] w-[95vw]
      ${transparent ? 'opacity-50' : 'opacity-100'}
    `}
  >
    <div
      class="h-[32px] w-[3px] bg-zinc-900 absolute -left-[17px] top-[72px] rounded-l-lg"
    ></div>
    <div
      class="h-[46px] w-[3px] bg-zinc-900 absolute -left-[17px] top-[124px] rounded-l-lg"
    ></div>
    <div
      class="h-[46px] w-[3px] bg-zinc-900 absolute -left-[17px] top-[178px] rounded-l-lg"
    ></div>
    <div
      class="h-[64px] w-[3px] bg-zinc-900 absolute -right-[17px] top-[142px] rounded-r-lg"
    ></div>
    <div class="rounded-[1.5rem] overflow-hidden h-full w-full bg-zinc-950">
      <slot />
    </div>
  </div>
</div>
