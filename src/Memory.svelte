<svelte:options customElement="wvn-jean-noel" />

<script lang="ts">
  import { onMount } from "svelte";

  let dialog: HTMLDialogElement;

  function showDialog() {
    dialog.showModal();
  }

  function handleKeyDown(event: KeyboardEvent) {
    if (event.key !== "Escape") return;

    dialog.close();
  }

  function handleClickOutside(event: MouseEvent) {
    const target = event.target as HTMLElement;
    if (target?.closest("a")) return;

    if (target !== dialog && !matchMedia("(max-width: 600px)").matches) return;

    dialog.close();
  }

  function handleClose() {
    localStorage.setItem("wvn-jean-noel", "true");
  }

  onMount(() => {
    if (localStorage.getItem("wvn-jean-noel") !== "true") {
      dialog.showModal();
    }
  });
</script>

<button class="ribbon" on:click={showDialog}> Jean-Noël Wallez </button>

<dialog
  on:keydown={handleKeyDown}
  bind:this={dialog}
  on:click={handleClickOutside}
  on:close={handleClose}
>
  <form method="dialog">
    <button class="close-button">✖</button>
    <article>
      <p>
        C’est avec une profonde tristesse que nous vous faisons part du décès de
        Jean-Noël Wallez, fondateur et administrateur de Wavenet.
      </p>

      <p>
        Au-delà du chef d'entreprise d'exception, Jean-Noël était une
        inspiration pour nous tous.
      </p>

      <p>
        Soyez certains que nos équipes continuent et continueront à vous fournir
        le service en respect des valeurs de qualité et de partenariat que
        Jean-Noël prônait avec passion et que nous partageons tous au sein de
        Wavenet.
      </p>

      <p>
        Pour vous permettre de témoigner votre soutien à la famille, une adresse
        email
        <a
          href="mailto:remembering-jean-noel@wavenet.be"
          target="_blank"
          rel="noopener noreferrer"
        >
          remembering-jean-noel@wavenet.be
        </a>
        a été ouverte.
      </p>

      <p>
        Le faire-part peut être consulté sur le
        <a
          href="https://vanhole.funeralmanager.rip/condoleance/fr/5f61ba9d8deb70.60585804,5fea2ff250cea1.81862168/6847d5b9d1475"
          target="_blank"
          rel="noopener noreferrer"
        >
          site du centre funéraire
        </a>.
      </p>
    </article>
  </form>
</dialog>

<style lang="scss">
  .ribbon {
    all: unset;
    position: fixed;
    top: 40px;
    right: -40px;
    width: 200px;
    height: 32px;
    background-color: black;
    color: #fff;
    rotate: 45deg;
    cursor: pointer;
    z-index: 10000;
    text-align: center;
    font:
      16px "Open Sans",
      Helvetica,
      Arial,
      sans-serif;
  }

  a {
    outline: 0;
    color: #3cf;
    text-decoration: none;
    transition: color 0.2s ease-in-out;
    &:hover,
    &:focus,
    &:active {
      outline: 0;
      color: #09c;
    }
  }

  dialog {
    box-sizing: border-box;
    border: #ccc;
    padding: 0;
    border-radius: 10px;
    font:
      16px "Open Sans",
      Helvetica,
      Arial,
      sans-serif;
  }

  form {
    position: relative;
    background: url("https://ik.imagekit.io/wavenet/jn-h.jpg") no-repeat right top/cover;
    width: 1000px;
    max-width: 100vw;
    min-height: 500px;
    max-height: 100dvh;
  }

  article {
    position: absolute;
    inset: 0 50% 0 0;
    background: rgba(0, 0, 0, 0.5);
    color: #fff;
    padding: 0 15px;
  }

  .close-button {
    all: unset;
    color: #000;
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 20px;
    cursor: pointer;
    z-index: 1000;
  }

  dialog::backdrop {
    background-color: rgba(0, 0, 0, 0.6);
    backdrop-filter: blur(5px);
  }

  @media (max-width: 600px) {
    .close-button {
      color: #fff;
    }
    form {
      position: fixed;
      inset: 0;
      height: 100%;
      min-height: unset;
      width: unset;
      height: unset;
      background: url("https://ik.imagekit.io/wavenet/jn-vert.jpg") no-repeat right top/cover;
      overflow-y: auto;
    }
    article {
      position: relative;
      margin-top: 400px;
      padding: 1px 20px;
    }
  }
</style>
