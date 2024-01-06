<script>
  export default {
    name: 'modalLis',
    props:[
        "name", 
        "price",
        "desc",
        "cat",
        "image",
        "rate",
        "count"],
    methods: {
      close() {
        this.$emit('close');
      },
    },
  };
</script>
<template>
    <transition name="modal-fade">
      <div class="modal-backdrop">
        <div class="modal"
          role="dialog"
          aria-labelledby="modalTitle"
          aria-describedby="modalDescription"
        >
          <header
            class="modal-header"
            id="modalTitle"
          >
            <slot name="header">
              {{ cat }}<br>{{name}}
  
              <button
                type="button"
                class="btn-close"
                @click="close"
                aria-label="Close modal"
              >
                x
              </button>
            </slot>
          </header>
          <section>
            <img :src="image" alt="картинка" class="header__img">
          </section>
          <section
            class="modal-body"
            id="modalDescription"
          >
            <slot name="body">
              {{ desc }}
            </slot>
          </section>
          <footer class="modal-footer">
            <slot name="footer">
              {{ price }} $
              <div class="footer__block">
                  <p>Рейтинг {{ rate }}</p>
                  <p>Голосовали {{ count }}</p>
              </div>
              <button
                type="button"
                class="btn-green"
                @click="close"
                aria-label="Close modal"
              >
                Close
              </button>
            </slot>
          </footer>
        </div>
      </div>
    </transition>
  </template>
<style>
  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: #FFFFFF;
    box-shadow: 2px 2px 20px 1px;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
  }

  .modal-header,
  .modal-footer {
    padding: 15px;
    display: flex;
  }

  .modal-header {
    border-bottom: 1px solid #eeeeee;
    color: #4AAE9B;
    justify-content: space-between;
  }

  .modal-footer {
    display: flex;
    align-items: center;
    border-top: 1px solid #eeeeee;
    justify-content:space-between;
  }
  .footer__block{
    display: flex;
    gap: 20px;
  }

  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    border: none;
    font-size: 20px;
    padding: 20px;
    cursor: pointer;
    font-weight: bold;
    color: #4AAE9B;
    background: transparent;
  }

  .btn-green {
    color: white;
    background: #4AAE9B;
    border: 1px solid #4AAE9B;
    border-radius: 2px;
  }

  .header__img{
    object-fit: contain;
    width: 250px;
    height: 200px;
  }
</style>