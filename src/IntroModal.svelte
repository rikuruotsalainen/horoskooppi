<script>
  export let showIntroModal = false; // State to control the modal visibility
  export let closeModal; // Function to close the modal
  export let introModalContent = {}; // Content to display in the modal
</script>

{#if showIntroModal}
  <div class="modal-overlay" on:click={closeModal}>
    <div class="modal-content" on:click|stopPropagation>
      <h2>{introModalContent.title}</h2>
      <p>{introModalContent.description}</p>
      <button on:click={closeModal}>Close</button>
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
    border-radius: 10px;
    width: 300px;
    text-align: center;
  }

  .modal-content button {
    margin-top: 10px;
  }
</style>
