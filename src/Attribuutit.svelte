<script>
  export let nimi;
  export let arvo;
  export let virhe;
  let onkoValidi = true;

  /* josYli ja josAlle -funktiot laskevat ominaisuusluvun (attribute score) pohjalta muuntimen (modifier).*/
  function josYli(x) {
    let y = (x - 10) / 2;
    if (y % 2 == 0) {
      return y;
    } else {
      y = Math.floor(y);
      return y;
    }
  }

  function josAlle(x) {
    let y = (x - 10) / 2;
    if (y % 2 == 0) {
      return y;
    } else {
      y = Math.floor(y);
      return y;
    }
  }
  /* Koodin validointi. Funktio katsoo, onko syötetty luku välillä 1–20. */
  const onkoValidiNumero = (z) => {
    return z > 0 && z < 21;
  };
</script>

<!--on:inputilla siirretään syötetty luku onkoValidiNumero-funktioon. Jos syöte ei ole validi, sen classiksi tulee "vaara", mikä vaikuttaa muotoiluun.-->
<label for="nimi">{nimi}</label>
<input
  type="number"
  bind:value={arvo}
  class:vaara={!onkoValidi}
  on:input={() => (onkoValidi = onkoValidiNumero(arvo))}
/>

<!--Vähän monimutkainen tapa tehdä yksinkertainen asia: lohko katsoo, onko luku yli vai alle 10 ja antaa sen mukaan ominaisuusmuuntimen eteen plusmerkin.-->
<div id="iffit">
  {#if arvo >= 10 && onkoValidi}
    +{josYli(arvo)}
  {:else if arvo <= 21 && onkoValidi}
    {josAlle(arvo)}
  {/if}
</div>

<!--Jos validointi ei mene läpi. Validointiosuuksiin on otettu hyvin vahvasti mallia kurssimateriaalista ja sovellettu siitä. -->
{#if virhe && !onkoValidi}
  <p class="virhe">{virhe}</p>
{/if}

<style>
  #iffit {
    color: #e9d8a6;
    margin: 5px;
    font-size: 1.2rem;
  }

  label {
    color: #e9d8a6;
    font-size: 1.15rem;
  }

  .virhe {
    color: #ca6702;
    margin: 5px;
    font-size: 1.2rem;
  }

  .vaara {
    border: 4px solid #b84a62;
  }
</style>
