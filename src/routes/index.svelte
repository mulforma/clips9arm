<script context="module">
  export async function load() {
    const url = 'https://raw.githubusercontent.com/thevvx/clips9arm/main/ENTRIES.md';
    const response = await fetch(url);

    return {
      status: response.status,
      props: {
        entries: (await response.text()),
      }
    }
  }
</script>

<script lang="ts">
  export let entries;

  let entryRegex = /- (?:\[(.*)\])(?:\((.*)\))/;
  entries = entries.split('\n').map(line =>
    entryRegex.test(line) ? line.match(entryRegex) : null
  ).filter(entry => entry !== null);
</script>


<div class='grid min-h-screen place-items-center dark:bg-black py-24'>
  <div class='flex flex-col gap-6'>
    <!-- Title -->
    <div class='flex flex-col items-center justify-center gap-3'>
      <h1 class='md:text-6xl text-5xl text-yellow-400 font-bold'>
        [ Clips9arm ]
      </h1>
      <p class='md:text-2xl text-lg text-slate-500 dark:text-slate-400'>
        แพลตฟอร์มที่ไว้รวบรวมคลิปเด็ดนายอาร์ม
      </p>
    </div>
    <!-- Clips List -->
    <div class='grid md:grid-cols-2 grid-cols-1 gap-2 place-items-center'>
      {#each entries as entry}
        <div class='flex flex-col gap-2 justify-center items-center border shadow-lg rounded-lg p-2'>
          <h2 class='text-xl font-bold dark:text-white' id={entry[1]}>
            <a href='#{entry[1]}'>
              {entry[1]}
            </a>
          </h2>
          <iframe
            src={ entry[2].split('/')[2] === "clips.twitch.tv" ? `https://clips.twitch.tv/embed?clip=${entry[2].split('/')[3]}&parent=clips9arm.vvx.bar` : entry[2] }
            frameborder="0"
            loading='lazy'
            allowfullscreen="true"
            scrolling="no"
            height="189"
            width="310">
          </iframe>
        </div>
      {/each}
    </div>
  </div>
</div>