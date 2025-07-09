<script>
  import { coordinator, clamp, scale } from "svelte-coordinator";

  let {
    width = "auto",
    min = 0,
    max = 100,
    value = $bindable([0, 100]),
  } = $props();

  let active = $state(-1);

  const handlers = {};

  handlers.onstart = ({ left, width }) => {
    active = value.findIndex(val => {
      let px = Math.round(scale(val, [min, max], [0, width]));
      return left >= px - 10 && left <= px + 10;
    });

    console.log(active)

    return active !== -1;
  };

  handlers.onaction = ({ left, width }) => {
    value[active] = clamp(Math.round(scale(left, [0, width], [min, max])), min, max);
  };

  handlers.onend = () => {
    active = -1;
  }
</script>

<div
class="range"
  {@attach coordinator(handlers)}
  style="width: {width}"
>
<div class="track"></div>
<div class="active-track" style="left: {scale(Math.min(...value), [min, max], [0, 100])}%; right: {100 -scale(Math.max(...value), [min, max], [0, 100])}%"></div>

{#each value as val, i}
  <i class="point" class:active={i === active} style="left: {scale(val, [min, max], [0, 100])}%"></i>
{/each}
</div>

<style>
  .range {
    position: relative;
    height: 20px;
    margin: 40px;
  }

  .track, .active-track {
    position: absolute;
    left: 0;
    right: 0;
    top: 50%;
    height: 4px;
    border-radius: 2px;
    transform: translateY(-50%);
    background-color: #dcdcdc;
  }

  .active-track {
    background-color: #fe0a63;
  }

  .point {
    position: absolute;
    top: 0;
    box-sizing: border-box;
    width: var(--size, 20px);
    height: var(--size, 20px);
    border-radius: 4px;
    border: 2px solid #fff;
    background-color: #e0e0e0;
    transform: translate(-50%);
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
  }

  .point.active {
    z-index: 100;
    background-color: #fe0a63;
  }
</style>
