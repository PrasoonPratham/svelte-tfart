<script>
  let avatar, fileinput;



  const onFileSelected = e => {
    let image = e.target.files[0];
    let reader = new FileReader();
    reader.readAsDataURL(image);
    reader.onload = e => {
      avatar = e.target.result;
    };
  };

  let avatar2, fileinput2;

  const onFileSelected2 = f => {
    let image2 = f.target.files[0];
    let reader = new FileReader();
    reader.readAsDataURL(image2);
    reader.onload = f => {
      avatar2 = f.target.result;
    };
  };



</script>

<div class="flex flex-row w-full">
  <div
    class="grid flex-grow h-full card bg-base-300 rounded-box place-items-center"
  >
    {#if avatar}
      <img class="avatar" src={avatar} alt="d" />
    {:else}
      <img
        class="avatar"
        src="https://cdn4.iconfinder.com/data/icons/small-n-flat/24/user-alt-512.png"
        alt=""
      />
    {/if}
    <img
      class="upload"
      src="https://static.thenounproject.com/png/625182-200.png"
      alt=""
      on:click={() => {
        fileinput.click();
      }}
    />
    <div
      class="chan"
      on:click={() => {
        fileinput.click();
      }}
    >
      Choose Image
    </div>
    <input
      style="display:none"
      type="file"
      accept=".jpg, .jpeg, .png"
      on:change={e => onFileSelected(e)}
      bind:this={fileinput}
    />
  </div>
</div>

<div class="divider divider-vertical py-11" />

<div
  class="grid flex-grow h-full card bg-base-300 rounded-box place-items-center"
>
  {#if avatar2}
    <img class="avatar" src={avatar2} alt="d" />
  {:else}
    <img
      class="avatar2"
      src="https://cdn4.iconfinder.com/data/icons/small-n-flat/24/user-alt-512.png"
      alt=""
    />
  {/if}
  <img
    class="upload"
    src="https://static.thenounproject.com/png/625182-200.png"
    alt=""
    on:click={() => {
      fileinput2.click();
    }}
  />
  <div
    class=""
    on:click={() => {
      fileinput2.click();
    }}
  >
    Choose Image
  </div>
  <input
    style="display:none"
    type="file"
    accept=".jpg, .jpeg, .png"
    on:change={f => onFileSelected2(f)}
    bind:this={fileinput2}
  />
</div>



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
