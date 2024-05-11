<script lang="ts">
  import products from "../data/index";

  let image: HTMLImageElement;

  function handleMouseOver() {
    const imagens = products[0].photos;
    let i = 0;

    function mostrarProximaImagem() {
      image.src = imagens[i];
      i = (i + 1) % imagens.length;
      timeoutId = setTimeout(mostrarProximaImagem, 1000);
    }

    let timeoutId = setTimeout(mostrarProximaImagem, 1000);

    image.addEventListener("mouseleave", () => {
      clearTimeout(timeoutId);
      image.src = imagens[0];
    });

    image.addEventListener("focus", () => {
      handleMouseOver();
    });
  }
</script>

<section
  role="button"
  tabindex="0"
  class="card"
  on:mouseover={handleMouseOver}
  on:focus={handleMouseOver}
>
  <figure class="card__image__container">
    <img
      class="card__image"
      bind:this={image}
      src={products[0].photos[0]}
      alt=""
    />
  </figure>
  <span class="card__text">
    <h3 class="card__text__Title">{products[0].name}</h3>
    <p class="card__text__price">{products[0].price}</p>
  </span>
</section>

<style>
  .card {
    width: 347px;
    height: 600px;
    cursor: pointer;
  }

  .card:hover .card__text {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }

  .card__image__container {
    width: 100%;
    height: 85%;
  }

  .card__image {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }

  .card__text {
    display: none;
    padding: 1rem 0px;
  }
</style>
