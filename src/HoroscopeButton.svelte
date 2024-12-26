<script>
  export let title;
  export let img;
  export let onClick;
</script>

<button on:click={onClick} class="horoscope-button">
  <!-- Horoskoopin kuva -->
  <img src={img} alt={title} />
  <!-- Horoskoopin nimi -->
  <span>{title}</span>
</button>

<!-- Tyylit -->
<style>
  .horoscope-button {
    align-items: center;
    display: flex;
    padding: 10px;
    margin: 10px;
    background-color: #3f3154;
    color: #aca3af;
    cursor: pointer;
    border-radius: 20px;
    border-width: 5px;
    font-size: x-large;
    font-weight: 500;
    border-color: #aca3af;
    border-style: solid;
    width: 400px;
    justify-content: space-between;
  }

  .horoscope-button img {
    width: 70px;
    height: 70px;
  }

  .horoscope-button:hover {
    background-color: #4a3c64;
  }
</style>
