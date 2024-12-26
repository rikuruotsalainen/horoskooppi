<script>
  import { horoscopeArray } from './horoscopeArray.js';
  import HoroscopeButton from './HoroscopeButton.svelte';
  import HoroscopeModal from './HoroscopeModal.svelte';
  import IntroModal from './IntroModal.svelte';

  let showModal = false;
  let modalContent = {};
  let isLoading = false;

  // The fetch function that uses itemId correctly
  async function fetchModalData(itemId) {
    isLoading = true;
    try {
      // Use a proxy to bypass CORS if needed
      const proxyUrl = 'https://api.allorigins.win/get?url=';
      const targetUrl = `https://horoscope-app-api.vercel.app/api/v1/get-horoscope/daily?sign=${itemId}&day=TODAY`;

      const response = await fetch(proxyUrl + encodeURIComponent(targetUrl));

      // Check if response is OK
      if (!response.ok) {
        throw new Error(`Error fetching data: ${response.statusText}`);
      }

      // Parse the response (the 'contents' field)
      const result = await response.json();
      const data = JSON.parse(result.contents); // Parse the stringified JSON in contents

      if (!data || !data.data) {
        throw new Error('Invalid response format');
      }

      // Set the modal content, including the date
      modalContent = {
        title: itemId, // Display the sign's name as title
        description: data.data.horoscope_data, // Display the horoscope data
        date: data.data.date, // Add the date here
        image: horoscopeArray.find((item) => item.id === itemId).image, // Find and set image
      };

      showModal = true; // Show the modal after fetching the data
    } catch (error) {
      console.error('Error fetching modal data:', error);
      modalContent = { title: 'Error', description: error.message };
      showModal = true; // Show error message in the modal
    } finally {
      isLoading = false;
    }
  }
  // Function to open the modal with specific content
  function openModal(item) {
    fetchModalData(item.id);
    modalContent = item; // Set the content to the selected item
    showModal = true; // Show the modal
  }

  // Close modal
  function closeModal() {
    showModal = false;
  }
</script>

<main>
  <h1>Horoskoopit</h1>
  <div class="button">
    {#each horoscopeArray as item}
      <HoroscopeButton
        title={item.id}
        img={item.image}
        onClick={() => openModal(item)}
      />
    {/each}
  </div>

  <!-- Modal component -->
  <HoroscopeModal {showModal} {closeModal} {modalContent} {isLoading} />
</main>

<style>
  main {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 20px;
  }

  /* 3 buttons per row */
  .button {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
    justify-content: center;
    align-items: center;
  }

  /* Responsiveness */
  @media (max-width: 1300px) {
    .button {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 800px) {
    .button {
      grid-template-columns: 1fr;
      justify-content: center;
    }
  }
</style>
