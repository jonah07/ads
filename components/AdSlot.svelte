<script>
  import { onMount } from "svelte";
  import { createEventDispatcher } from "svelte";

  export let backgroundColor;

  let time;
  let moving = false;
  let left = 0;
  const breakpoints = Array.from({ length: 12 }, (_, i) => (i + 1) * 50);

  const dispatch = createEventDispatcher();

  function findNumberNear(array, number, threshold) {
    for (let i = 0; i < array.length; i++) {
      if (Math.abs(array[i] - number) <= threshold) {
        return array[i];
      }
    }
    return null;
  }

  function calculateMagnetizedWidth() {
    const magnetizedWidth = time.style.width.replace("px", "");
    const nearest = findNumberNear(breakpoints, magnetizedWidth, 30);

    if (nearest) {
      time.style.width = nearest + "px";
    }
  }

  onMount(() => {
    const resizeObserver = new ResizeObserver(entries => {
      for (const entry of entries) {
      }
    });

    const greenDiv = document.querySelector(".resize-x");
    resizeObserver.observe(greenDiv);

    return () => {
      resizeObserver.unobserve(greenDiv);
      resizeObserver.disconnect();
    };
  });

  function onMouseUp() {
    calculateMagnetizedWidth();
    dispatch("mouseup");
  }

  function movingOnMouseDown() {
    moving = true;
  }

  function movingOnMouseMove(e) {
    if (moving) {
      const tleft = left + 0;
      const newLeft = tleft + e.movementX;
      if (newLeft > 0 && newLeft < 600 - time.style.width.replace("px", "")) {
        left = newLeft;
      }
    }
  }

  function movingOnMouseUp() {
    moving = false;
  }

  function movingOnMouseLeave() {
    moving = false;
  }
</script>

<div
  on:mouseup={onMouseUp}
  on:mousemove={movingOnMouseMove}
  on:mouseleave={movingOnMouseLeave}
  bind:this={time}
  class="resize-x max-w-[600px] text-white overflow-hidden mt-2 h-[50px] rounded-md p-2 text-xs cursor-move {backgroundColor}"
  style="margin-left: {left}px"
>
  <span
    on:mouseup={movingOnMouseUp}
    on:mousedown={movingOnMouseDown}
    class="truncate select-none text-white overflow-none h-full w-full block"
  >
  <slot></slot>
  </span>
</div>
