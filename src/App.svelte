<script>
  import Attribuutit from './Attribuutit.svelte';
  export let name;

  /* Ominaisuuksien lähtöarvot. Arvo-muuttujat on sidottu kaksisuuntaisesti input-kenttään. */
  let ominaisuudet = [
    {
      id: 'Voimakkuus',
      arvo: 10,
    },
    { id: 'Kestävyys', arvo: 10 },
    {
      id: 'Ketteryys',
      arvo: 10,
    },
    { id: 'Älykkyys', arvo: 10 },
    {
      id: 'Viisaus',
      arvo: 10,
    },
    {
      id: 'Karisma',
      arvo: 10,
    },
  ];

  /* Funktio arpoo neljä satunnaista arvoa väliltä 1–6, katsoo niistä pienimmän ja poistaa sen. Tämän jälkeen kolme jäljellä olevaa arvoa lasketaan yhteen ja summa 
  asetetaan objektin arvo-elementtiin.
  Tämä simuloi neljän kuusikylkisen nopan heittoa, josta p-elementissä puhutaan. */
  function rollaaArvo(n) {
    let luvut = [];
    for (let i = 0; i < 4; i++) {
      let luku = Math.floor(Math.random() * 6) + 1;
      luvut.push(luku);
    }
    let y = Math.min(...luvut);
    luvut.splice(luvut.indexOf[y], 1);
    let summa = luvut.reduce((a, b) => a + b);
    ominaisuudet[n].arvo = summa;
  }
</script>

<body>
  <main>
    <div id="maincontainer">
      <h1>{name}</h1>
      <p>
        Onnittelut ensimmäisestä askeleestasi pöytäroolipelien maailmaan! Tämä
        sivusto auttaa sinua pisteyttämään pelihahmosi.
        <br /><br />
        Aloita syöttämällä hahmosi ominaisuuspisteet. Tyypillisesti ominaisuudet
        heitetään pyöräyttämällä neljää kuusisivuista noppaa, pudottamalla alin silmäluku
        pois ja laskemalla jäävät kolme silmälukua yhteen.
        <br /><br />
        Jos saatavilla ei ole noppia, voit käyttää nopanheittopainikkeita tai – poikkeuksellisesti,
        tämä ei ole hyvää roolipelikäytäntöä – keksiä luvut päästäsi.
        <br /><br />
        Ohjelma antaa sinulle ominaisuusmuuntimet, jotka lisätään taitoheittoihin.
      </p>

      <!-- each-elementti käy läpi ominaisuudet-taulukon objektit. Jos Attribuutit-komponentissa tehtävä validaatio ei onnistu, sivu antaa virheilmoituksen.
      Kun testasin koodia palautusdeadlinea edeltävänä iltana, huomasin, että jos rollaaArvo-funktio suoritetaan virheilmoituksen saamisen jälkeen, onkoValidi ei palaa
      trueksi, vaan virheilmoitus pysyy. Vain syötteen muuttaminen manuaalisesti takaisin hyväksyttävälle välille (1–20) poistaa virheilmoituksen. En tällä ajalla 
      oikein tiedä, kuinka ongelma on ratkaistavissa. -->
      <div id="kentät">
        {#each ominaisuudet as ominaisuus, i}
          <Attribuutit
            bind:arvo={ominaisuus.arvo}
            nimi={ominaisuus.id}
            virhe="Valitse numero väliltä 1–20!"
          />
          <!-- Painikkeen napsauttaminen kutsuu rollaaArvo-funktiota. -->
          <button on:click={() => rollaaArvo(i)}>Heitä noppaa</button>
        {/each}
      </div>
    </div>
  </main>
</body>

<style>
  body {
    max-width: 100%;
    margin: auto;
  }

  main {
    text-align: center;
    padding: 1em;
    background-color: #94d2bd;
  }

  h1 {
    color: #e9d8a6;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  p {
    width: 40%;
    margin: auto;
    color: #e9d8a6;
    font-size: 1.2rem;
  }

  button {
    margin-top: 10px;
    margin-bottom: 30px;
    background-color: #94d2bd;
    border: 1px solid #0a9396;
    color: #001219;
    padding: 11px;
  }

  #maincontainer {
    max-width: 50%;
    margin: auto;
    border: 4px solid #0a9396;
    background-color: #005f73;
  }

  #kentät {
    width: 30%;
    margin: auto;
    padding-top: 40px;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
