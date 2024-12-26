<script>
  export let showModal = false;
  export let closeModal;
  export let modalContent = {};
  export let isLoading = false;
  import { fly, fade, scale } from 'svelte/transition';
</script>

<!-- Vain jos modaali on näkyvissä -->
{#if showModal}
  <div class="overlay">
    <div class="content" transition:scale={{ duration: 300 }}>
      <!-- Lataus teksti -->
      {#if isLoading}
        <p>Loading...</p>
      {:else}
        <!-- Valitun horoskoopin nimi -->
        <h1>{modalContent.title}</h1>
        <!-- Horoskoopin päivämäärä saatu fetchistä -->
        <h2>{modalContent.date}</h2>
        <!-- Horoskoopin kuva -->
        <img src={modalContent.image} alt={modalContent.title} />
        <!-- Fecthistä saatu tieto -->
        <div class="description">
          <p>{modalContent.description}</p>
        </div>
        <!-- Nappi joka sulkee modaalin -->
        <button on:click={closeModal} class="button">Close</button>
      {/if}
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
    width: 50%;
    text-align: center;
    border-color: #aca3af;
    border-style: solid;
    border-radius: 20px;
    border-width: 3px;
  }
  .content img {
    max-width: 100%;
    height: auto;
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
  p {
    font-size: large;
  }
  .description {
    justify-content: center;
    align-items: center;
    width: 80%;
    border-color: #aca3af;
    border-radius: 20px;
    border-width: 3px;
    border-style: solid;
    margin-left: 5%;
    margin-top: 3%;
    margin-bottom: 3%;
    padding: 5%;
  }
</style>
