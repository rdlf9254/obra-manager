<template>
  <section v-if="showModal" class="modal">
    <div @click="close()" class="overlay"></div>

    <div class="modal-box">
      <a @click="close()" class="close">×</a>
      <div v-if="title" class="title">
        <h3>{{ title }}</h3>
      </div>

      <div class="modal-cont">
        <slot name="content"></slot>
      </div>

      <div class="modal-ac">
        <slot name="action"></slot>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "modal",
  props: {
    show: {
      default: false,
      required: true,
    },
    title: {
      default: "",
      required: false,
    },
  },
  data() {
    return {
      showModal: false,
    };
  },
  watch: {
    show(value) {
      this.showModal = value;
    },
  },
  mounted() {
    this.showModal = this.show;
  },
  methods: {
    close() {
      this.showModal = false;
      this.$emit("close");
    },
  },
};
</script>

<style lang="scss" scoped>
section.modal {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;

  .overlay {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(
      circle,
      rgba(0, 0, 0, 0.8) 10%,
      rgba(0, 0, 0, 0.8) 50%,
      #000 100%
    );
    z-index: -1;
  }

  .modal-box {
    width: 90%;
    max-width: 650px;
    max-height: 95vh;
    padding: var(--4sxl) var(--5sxl);
    position: relative;
    overflow-y: scroll;
    background: var(--white);
    z-index: 99;
    box-shadow: 0 3px var(--sl) rgba(black, 0.4);

    a.close {
      font-size: var(--2sxl2);
      position: absolute;
      right: var(--sxl);
      top: var(--sm);
      cursor: pointer;
    }

    .title {
      text-align: center;
      margin-bottom: var(--4sxl);

      h3 {
        font-size: 2.3rem;
        font-weight: 600;
      }

      p {
        max-width: 500px;
        margin: 5px auto 0;
        font-size: 1.7rem;
        opacity: 0.8;
      }
    }
  }
}
</style>
