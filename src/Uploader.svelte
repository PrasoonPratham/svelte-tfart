<script>
  import * as mi from '@magenta/image';
  import {onMount} from 'svelte';

  const model = new mi.ArbitraryStyleTransferNetwork();

  const contentImg = document.getElementById('content');
  const styleImg = document.getElementById('style');
  let canvas, ctx;

  onMount(() => {
    ctx = canvas.getContext('2d');
  });

  async function stylize() {
    await clearCanvas();

    // Resize the canvas to be the same size as the source image.
    canvas.width = contentImg.width;
    canvas.height = contentImg.height;

    // This does all the work!
    model.stylize(contentImg, styleImg).then(imageData => {
      ctx.putImageData(imageData, 0, 0);
    });
  }

  async function clearCanvas() {
    // Don't block painting until we've reset the state.
    await mi.tf.nextFrame();
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    await mi.tf.nextFrame();
  }

	let  avatar, fileinput;
	
	const loadImage =(e)=>{
  let image = e.target.files[0];
            let reader = new FileReader();
            reader.readAsDataURL(image);
            reader.onload = e => {
                 e = e.target.result
            };
}

  function loadContent(e) {
    loadImage(e);
  }

  function loadStyle(event) {
    loadImage(event, styleImg);
  }
</script>

<div class="frame">
  <label>upload photo <input type="file" on:click={loadContent(event)} /></label
  >

  <!-- svelte-ignore a11y-missing-attribute -->
  <img
    id="content"
    class="image"
    crossorigin="anonymous"
    src='{contentImg}'
  />
</div>

<div class="frame">
  <label>upload photo <input type="file" on:click={loadStyle(event)} /></label
  >
  <!-- svelte-ignore a11y-missing-attribute -->
  <img
    id="style"
    class="image"
    crossorigin="anonymous"
    src="https://cdn.glitch.com/93893683-46da-4058-829c-a05792722f2b%2Fcontent.jpg?1545163443723"
  />
</div>

<canvas id="stylized" bind:this={canvas} width={480} height={320} />

<div class="py-8 px-8">
  <div class="alert">
    <div class="flex-1">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke="#009688"
        class="flex-shrink-0 w-6 h-6 mx-2"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
        />
      </svg>
      <div>
        <h4>Pro Tip</h4>
        <p class="text-sm text-base-baseImg text-opacity-60">
          Certain cobinations of style and base images work beter than others,
          feel free to experiment and play around as much as you like!
        </p>
      </div>
    </div>
  </div>
</div>
