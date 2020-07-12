<style>
  .modal-container {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-color: hsla(0, 0%, 0%, 0.58);
  }

  .modal-content {
    padding: 2rem;
    background-color: white;
  }
</style>

<section>
  <div class="modal-container">
    <div class="modal-content">
      <slot>
        <!--optional fallback-->
      </slot>
    </div>
  </div>
</section>
