<!-- Modaali joka tulee näkyviin kun sivu avataan -->
<script>
  import { createEventDispatcher } from 'svelte';
  import { horoscopeArray } from './horoscopeArray.js';
  import { fly, fade, scale } from 'svelte/transition';
  export let showIntroModal = false;
  export let closeIntroModal;

  const dispatch = createEventDispatcher();

  let selectedOption = '';

  // Funktio joka hallitsee horoskooppien valitsemisen
  function handleDropdownChange(event) {
    selectedOption = event.target.value;
    dispatch('select', selectedOption); // Dispatch the selected zodiac sign to the parent
  }

  // Haetaan valitun horoskoopin kuva
  function getSelectedImage() {
    const selectedSign = horoscopeArray.find(
      (item) => item.id === selectedOption
    );
    return selectedSign ? selectedSign.image : '';
  }
  // Haetaan valitun horoskoopin päivämäärä
  function getSelectedDate() {
    const selectedSign = horoscopeArray.find(
      (item) => item.id === selectedOption
    );
    return selectedSign ? selectedSign.date : '';
  }
</script>

<!-- Vain jos modaali on näkyvissä -->
{#if showIntroModal}
  <div class="overlay">
    <div class="content" transition:scale={{ duration: 300 }}>
      <h1>Welcome to the Horoscope App!</h1>
      <p>This app lets you check daily horoscopes for your zodiac sign.</p>

      <!-- Valikko horoskoopin valitsemiseksi -->
      <label for="zodiac">Select your horoscope:</label>
      <select
        id="zodiac"
        bind:value={selectedOption}
        on:change={handleDropdownChange}
        required
      >
        <option value="" disabled selected>Select a sign</option>
        <!-- Tulostetaan kaikki horoskoopit horoscopeArray taulukosta valikon vaihtoehdoiksi -->
        {#each horoscopeArray as option}
          <option value={option.id}>{option.id}</option>
        {/each}
      </select>
      <!-- Horoskoopin nimi -->
      <h3>Your selected sign is: {selectedOption}</h3>

      <!-- Näytetään valitun horoskoopin kuva ja päivämäärä sitten kun horoskooppi on valittu -->
      {#if selectedOption}
        <div>
          <!-- Horoskoopin kuva -->
          <img
            src={getSelectedImage()}
            alt={selectedOption}
            style="width: 70px; height: 70px;"
          />
          <!-- Horoskoopin päivämäärä -->
          <h3>{getSelectedDate()}</h3>
        </div>
      {/if}
      <!-- Nappi joka sulkee modaalin pois päältä siihen asti kunnes horoskooppi on valittu -->
      <button
        on:click={closeIntroModal}
        class="button"
        disabled={!selectedOption}>Select</button
      >
    </div>
  </div>
{/if}

<!-- Tyylit -->
<style>
  .overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.9);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }

  .content {
    background: #3f3154;
    padding: 20px;
    border-radius: 10px;
    width: 300px;
    text-align: center;
  }

  select {
    margin: 10px 0;
    padding: 5px;
    width: 100%;
    font-size: 16px;
    border-radius: 5px;
  }

  button {
    background-color: #3f3154;
    color: #aca3af;
    font-size: large;
    width: 50%;
    margin-top: 10px;
    height: 50px;
    border-color: #aca3af;
    border-radius: 20px;
    border-style: solid;
    border-width: 5px;
    cursor: pointer;
  }

  .button:hover {
    background-color: #4a3c64;
  }
  .button:disabled {
    background-color: #6b5a7d;
    cursor: not-allowed;
    opacity: 0.7;
  }
  p {
    font-size: large;
  }
</style>
