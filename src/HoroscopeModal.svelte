<script>
  export let showModal = false;
  export let closeModal;
  export let modalContent = {};
  export let isLoading = false;
</script>

{#if showModal}
  <div class="modal-overlay" on:click={closeModal}>
    <div class="modal-content" on:click|stopPropagation>
      {#if isLoading}
        <p>Loading...</p>
      {:else}
        <h1>{modalContent.title}</h1>
        <h2>{modalContent.date}</h2>
        <img src={modalContent.image} alt={modalContent.title} />
        <p>{modalContent.description}</p>
        <button on:click={closeModal} class="button">Close</button>
      {/if}
    </div>
  </div>
{/if}

<style>
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.8);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
  }

  .modal-content {
    background: #3f3154;
    padding: 20px;
    width: 50%;
    text-align: center;
    border-color: #aca3af;
    border-radius: 20px;
    border-width: 5px;
  }
  .modal-content img {
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
    border-width: 5px;
    cursor: pointer;
  }
  .button:hover {
    background-color: #4a3c64;
  }
</style>
