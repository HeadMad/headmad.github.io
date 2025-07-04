<script>
  import { coordinator, clamp, scale } from "svelte-coordinator";

  let {
    width = "auto",
    min = 0,
    max = 100,
    value = $bindable([0, 100]),
  } = $props();

  let active = -1;

  const handlers = {};

  handlers.onstart = ({ left, width }) => {
    let mn = Math.round(scale(value[0], [min, max], [0, width]));
    
    if ((left >= mn - 10 && left <= mn + 10)) 
    return active = 0;

    let mx = Math.round(scale(value[1], [min, max], [0, width]));
    if (left >= mx - 10 && left <= mx + 10)
      return active = 1;

    return false;
    
  };

  handlers.onaction = ({ left, width }) => {
    if (active) 
    value[1] = clamp(Math.round(scale(left, [0, width], [min, max])), value[0], max);

    else
    value[0] = clamp(Math.round(scale(left, [0, width], [min, max])), min, value[1]);
  };
</script>

<div
  {@attach coordinator(handlers)}
  style="--xMin: {scale(value[0], [min, max], [0, 100])}%; --xMax: {scale(
    value[1],
    [min, max],
    [0, 100],
  )}%; width: {width}"
>
  <i class="min"></i>
  <i class="max"></i>
</div>

<style>
  div {
    position: relative;
    height: 20px;
    margin: 40px;
  }

  div::before {
    content: "";
    position: absolute;
    top: 50%;
    height: 4px;
    width: 100%;
    border-radius: 2px;
    transform: translateY(-50%);
    background-color: #989899;
  }

  .min,
  .max {
    position: absolute;
    top: 0;
    left: var(--xMin);
    width: var(--size, 20px);
    height: var(--size, 20px);
    border-radius: 50%;
    background-color: white;
    transform: translate(-50%);
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
  }

  .max {
    left: var(--xMax);
  }
</style>
