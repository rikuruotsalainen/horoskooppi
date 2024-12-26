<script>
  //importit
  import { horoscopeArray } from './horoscopeArray.js';
  import HoroscopeButton from './HoroscopeButton.svelte';
  import HoroscopeModal from './HoroscopeModal.svelte';
  import IntroModal from './IntroModal.svelte';

  let showModal = false; //Horoskooppi data modaali on piilotettu ennen kuin nappia painetaan
  let showIntroModal = true; // Intro modaali jossa käyttäjä valitsee oman horoskooppinsa on heti näkyvissä
  let modalContent = {}; // Modaalin sisältö on aluksi tyhjä koska fetchiä ei ole tehty
  let isLoading = false; //Lataus teksti ei tule näkyviin ennen kuin sitä kutsutaan
  let selectedZodiac = null; // Talennetaan valittu horoskooppi

  function handleZodiacSelect(event) {
    selectedZodiac = horoscopeArray.find((item) => item.id === event.detail); // Etsitään koko horoskoopin tiedot valitun nimen perusteella
  }

  // Fetchaa horoskoopin datan valitulle horoskoopille
  async function fetchModalData(itemId) {
    // Lataus teksti näkyy sillä aikaa kun dataa ladataan
    isLoading = true;
    try {
      // Tässä käytetty AI koska en osannut mennä CORS errorin ohi fetchissä ilman sitä
      // AI käytti api.allorigins.win proxya joka ohtti CORS errorin
      const proxyUrl = 'https://api.allorigins.win/get?url=';
      //halutun fetchin URL
      const targetUrl = `https://horoscope-app-api.vercel.app/api/v1/get-horoscope/daily?sign=${itemId}&day=TODAY`;
      // Muuten normaali fetch mutta siinä yhdistetään proxyUrl ja targetUrl
      const response = await fetch(proxyUrl + encodeURIComponent(targetUrl));
      //Error viesti
      if (!response.ok) {
        throw new Error(`Error fetching data: ${response.statusText}`);
      }

      const result = await response.json();
      const data = JSON.parse(result.contents);

      if (!data || !data.data) {
        throw new Error('Invalid response format');
      }

      modalContent = {
        title: itemId, // Näytetään horoskoopin nimi otsikkona
        description: data.data.horoscope_data, // Fetchistä saatu päivän horoskooppi
        date: data.data.date, // Fetchistä saatu horoskoopin päivämäärä
        image: horoscopeArray.find((item) => item.id === itemId)?.image || '', // Etsitään horoskoopin kuva mikä vastaa nimeä
      };

      showModal = true; // Näytetään modaali
      //Error viesti
    } catch (error) {
      console.error('Error fetching modal data:', error);
      modalContent = { title: 'Error', description: error.message };
      showModal = true;
      //Latausteksti pois
    } finally {
      isLoading = false;
    }
  }

  // Function to open the modal with specific content
  function openModal(item) {
    fetchModalData(item.id); // Only call fetchModalData, no need to set modalContent here again
  }

  // funktio joka sulkee horoskooppi tieto modaalin
  function closeModal() {
    showModal = false;
  }

  // Funktio joka sulkee aloitus modaalin
  function closeIntroModal() {
    showIntroModal = false;
  }
</script>

<main>
  <h1>My Horoscope</h1>

  <!-- Luo napin käyttäjän valitsemalle horoskoopille -->
  {#if selectedZodiac}
    <HoroscopeButton
      title={selectedZodiac.id}
      img={selectedZodiac.image}
      onClick={() => openModal(selectedZodiac)}
    />
  {/if}

  <h1>All Horoscopes</h1>
  <!-- Kaikki horoskoopit jos käyttäjä haluaa lukea muita kuin omaa -->
  <div class="button">
    <!-- Luo napin horoscopeArrayn jokaiselle horoskoopille -->
    {#each horoscopeArray as item}
      <HoroscopeButton
        title={item.id}
        img={item.image}
        onClick={() => openModal(item)}
      />
    {/each}
  </div>

  <!-- Modaali joka aukeaa sivun auetessa -->
  <IntroModal
    {showIntroModal}
    {closeIntroModal}
    on:select={handleZodiacSelect}
  />

  <!-- Horoskooppi tieto modaali joka aukeaa nappia painamalla -->
  <HoroscopeModal {showModal} {closeModal} {modalContent} {isLoading} />
</main>

<!-- Tyylit/responsiivisuus -->
<style>
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 20px;
  }

  /* 3 nappia per rivi*/
  .button {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
    justify-content: center;
    align-items: center;
  }

  /* Responsiivisuus 2 nappia per rivi pienemällä näytöllä */
  @media (max-width: 1300px) {
    .button {
      grid-template-columns: repeat(2, 1fr);
    }
  }
  /* Responsiivisuus 1 nappi per rivi pienemällä näytöllä */
  @media (max-width: 800px) {
    .button {
      grid-template-columns: 1fr;
      justify-content: center;
    }
  }
</style>
