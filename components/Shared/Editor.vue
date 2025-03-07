<template>
  <medium-editor
    v-if="show"
    :text="text"
    :options="options"
    placeholder="تجربه کاری"
    @edit="applyTextEdit"
  />
</template>

<script>
import MediumEditor from 'vue2-medium-editor'

export default {
  components: {
    MediumEditor,
  },
  props: {
    value: {
      type: String,
      default: '',
      required: true,
    },
  },
  data: () => ({
    text: '',
    show: true,
    tag: 'h1',
    options: {
      targetBlank: true,
      forcePlainText: true,
      toolbar: {
        buttons: ['bold', 'italic', 'underline', 'h2', 'h3', 'unorderedlist'],
        diffTop: -50,
        static: false,
        /* options which only apply when static is true */
        align: 'center',
        sticky: true,
        updateOnEmptySelection: false,
      },
      placeholder: {
        text: '',
      },
    },
    optionsValid: true,
  }),
  watch: {
    text(newValue, oldValue) {
      this.$emit('input', newValue)
    },
  },
  mounted() {
    this.text = this.value
  },
  methods: {
    applyTextEdit(ev) {
      if (ev.event.target) {
        this.text = ev.event.target.innerHTML
      }
    },
  },
}
</script>

<style lang="scss" scoped>
.medium-editor-element {
  width: 100%;
  height: 300px;
  /* direction: rtl; */
  border: 2px solid #dcdfe6;
  border-radius: 4px;
  transition: border-color 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
  outline: none;
  padding: 5px 10px;
  overflow-y: auto;
  ::v-deep {
    p {
      margin: 0 2px;
      line-height: 25px;
      font-size: 13px;
    }
    h2 {
      font-size: 18px;
      font-weight: 500;
    }
    h3 {
      font-size: 15px;
      font-weight: 500;
    }
  }
}
.medium-editor-element:focus,
.medium-editor-element:active {
  border-color: $--color-primary;
}
</style>

<style>
@-webkit-keyframes medium-editor-image-loading {
  0% {
    -webkit-transform: scale(0);
    transform: scale(0);
  }
  100% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }
}

@keyframes medium-editor-image-loading {
  0% {
    -webkit-transform: scale(0);
    transform: scale(0);
  }
  100% {
    -webkit-transform: scale(1);
    transform: scale(1);
  }
}

@-webkit-keyframes medium-editor-pop-upwards {
  0% {
    opacity: 0;
    -webkit-transform: matrix(0.97, 0, 0, 1, 0, 12);
    transform: matrix(0.97, 0, 0, 1, 0, 12);
  }
  20% {
    opacity: 0.7;
    -webkit-transform: matrix(0.99, 0, 0, 1, 0, 2);
    transform: matrix(0.99, 0, 0, 1, 0, 2);
  }
  40% {
    opacity: 1;
    -webkit-transform: matrix(1, 0, 0, 1, 0, -1);
    transform: matrix(1, 0, 0, 1, 0, -1);
  }
  100% {
    -webkit-transform: matrix(1, 0, 0, 1, 0, 0);
    transform: matrix(1, 0, 0, 1, 0, 0);
  }
}

@keyframes medium-editor-pop-upwards {
  0% {
    opacity: 0;
    -webkit-transform: matrix(0.97, 0, 0, 1, 0, 12);
    transform: matrix(0.97, 0, 0, 1, 0, 12);
  }
  20% {
    opacity: 0.7;
    -webkit-transform: matrix(0.99, 0, 0, 1, 0, 2);
    transform: matrix(0.99, 0, 0, 1, 0, 2);
  }
  40% {
    opacity: 1;
    -webkit-transform: matrix(1, 0, 0, 1, 0, -1);
    transform: matrix(1, 0, 0, 1, 0, -1);
  }
  100% {
    -webkit-transform: matrix(1, 0, 0, 1, 0, 0);
    transform: matrix(1, 0, 0, 1, 0, 0);
  }
}

.medium-editor-anchor-preview {
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-size: 16px;
  left: 0;
  line-height: 1.4;
  max-width: 280px;
  position: absolute;
  text-align: center;
  top: 0;
  word-break: break-all;
  word-wrap: break-word;
  visibility: hidden;
  z-index: 2000;
}
.medium-editor-anchor-preview a {
  color: #fff;
  display: inline-block;
  margin: 5px 5px 10px;
}

.medium-editor-anchor-preview-active {
  visibility: visible;
}

.medium-editor-dragover {
  background: #ddd;
}

.medium-editor-image-loading {
  -webkit-animation: medium-editor-image-loading 1s infinite ease-in-out;
  animation: medium-editor-image-loading 1s infinite ease-in-out;
  background-color: #333;
  border-radius: 100%;
  display: inline-block;
  height: 40px;
  width: 40px;
}

.medium-editor-placeholder {
  position: relative;
}
.medium-editor-placeholder:after {
  content: attr(data-placeholder) !important;
  font-style: italic;
  position: absolute;
  left: 0;
  top: 0;
  white-space: pre;
  padding: inherit;
  margin: inherit;
}

.medium-editor-placeholder-relative {
  position: relative;
}
.medium-editor-placeholder-relative:after {
  content: attr(data-placeholder) !important;
  font-style: italic;
  position: relative;
  white-space: pre;
  padding: inherit;
  margin: inherit;
}

.medium-toolbar-arrow-under:after,
.medium-toolbar-arrow-over:before {
  border-style: solid;
  content: '';
  display: block;
  height: 0;
  left: 50%;
  margin-left: -8px;
  position: absolute;
  width: 0;
}

.medium-toolbar-arrow-under:after {
  border-width: 8px 8px 0 8px;
}

.medium-toolbar-arrow-over:before {
  border-width: 0 8px 8px 8px;
  top: -8px;
}

.medium-editor-toolbar {
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-size: 16px;
  left: 0;
  position: absolute;
  top: 0;
  visibility: hidden;
  z-index: 2000;
}
.medium-editor-toolbar ul {
  margin: 0;
  padding: 0;
}
.medium-editor-toolbar li {
  float: left;
  list-style: none;
  margin: 0;
  padding: 0;
}
.medium-editor-toolbar li button {
  box-sizing: border-box;
  cursor: pointer;
  display: block;
  font-size: 14px;
  line-height: 1.33;
  margin: 0;
  padding: 15px;
  text-decoration: none;
}
.medium-editor-toolbar li button:focus {
  outline: none;
}
.medium-editor-toolbar li .medium-editor-action-underline {
  text-decoration: underline;
}
.medium-editor-toolbar li .medium-editor-action-pre {
  font-family: Consolas, 'Liberation Mono', Menlo, Courier, monospace;
  font-size: 12px;
  font-weight: normal;
  padding: 15px 0;
}

.medium-editor-toolbar-active {
  visibility: visible;
}

.medium-editor-sticky-toolbar {
  position: fixed;
  top: 1px;
}

.medium-editor-relative-toolbar {
  position: relative;
}

.medium-editor-toolbar-active.medium-editor-stalker-toolbar {
  -webkit-animation: medium-editor-pop-upwards 160ms forwards linear;
  animation: medium-editor-pop-upwards 160ms forwards linear;
}

.medium-editor-action-bold {
  font-weight: bolder;
}

.medium-editor-action-italic {
  font-style: italic;
}

.medium-editor-toolbar-form {
  display: none;
}
.medium-editor-toolbar-form input,
.medium-editor-toolbar-form a {
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
}
.medium-editor-toolbar-form .medium-editor-toolbar-form-row {
  line-height: 14px;
  margin-left: 5px;
  padding-bottom: 5px;
}
.medium-editor-toolbar-form .medium-editor-toolbar-input,
.medium-editor-toolbar-form label {
  border: none;
  box-sizing: border-box;
  font-size: 14px;
  margin: 0;
  padding: 6px;
  width: 316px;
  display: inline-block;
}
.medium-editor-toolbar-form .medium-editor-toolbar-input:focus,
.medium-editor-toolbar-form label:focus {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  border: none;
  box-shadow: none;
  outline: 0;
}
.medium-editor-toolbar-form a {
  display: inline-block;
  font-size: 24px;
  font-weight: bolder;
  margin: 0 10px;
  text-decoration: none;
}

.medium-editor-toolbar-form-active {
  display: block;
}

.medium-editor-toolbar-actions:after {
  clear: both;
  content: '';
  display: table;
}

.medium-editor-element {
  word-wrap: break-word;
  min-height: 30px;
}
.medium-editor-element img {
  max-width: 100%;
}
.medium-editor-element sub {
  vertical-align: sub;
}
.medium-editor-element sup {
  vertical-align: super;
}

.medium-editor-hidden {
  display: none;
}

.medium-toolbar-arrow-under:after {
  border-color: #242424 transparent transparent transparent;
  top: 50px;
}

.medium-toolbar-arrow-over:before {
  border-color: transparent transparent #242424 transparent;
  top: -8px;
}

.medium-editor-toolbar {
  background-color: #242424;
  background: -webkit-linear-gradient(top, #242424, rgba(36, 36, 36, 0.75));
  background: linear-gradient(to bottom, #242424, rgba(36, 36, 36, 0.75));
  border: 1px solid #000;
  border-radius: 5px;
  box-shadow: 0 0 3px #000;
}
.medium-editor-toolbar li button {
  background-color: #242424;
  background: -webkit-linear-gradient(top, #242424, rgba(36, 36, 36, 0.89));
  background: linear-gradient(to bottom, #242424, rgba(36, 36, 36, 0.89));
  border: 0;
  border-right: 1px solid #000;
  border-left: 1px solid #333;
  border-left: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 2px 2px rgba(0, 0, 0, 0.3);
  color: #fff;
  height: 50px;
  min-width: 50px;
  -webkit-transition: background-color 0.2s ease-in;
  transition: background-color 0.2s ease-in;
}
.medium-editor-toolbar li button:hover {
  background-color: #000;
  color: yellow;
}
.medium-editor-toolbar li .medium-editor-button-first {
  border-bottom-left-radius: 5px;
  border-top-left-radius: 5px;
}
.medium-editor-toolbar li .medium-editor-button-last {
  border-bottom-right-radius: 5px;
  border-top-right-radius: 5px;
}
.medium-editor-toolbar li .medium-editor-button-active {
  background-color: #000;
  background: -webkit-linear-gradient(top, #242424, rgba(0, 0, 0, 0.89));
  background: linear-gradient(to bottom, #242424, rgba(0, 0, 0, 0.89));
  color: #fff;
}

.medium-editor-toolbar-form {
  background: #242424;
  border-radius: 5px;
  color: #999;
}
.medium-editor-toolbar-form .medium-editor-toolbar-input {
  background: #242424;
  box-sizing: border-box;
  color: #ccc;
  height: 50px;
}
.medium-editor-toolbar-form a {
  color: #fff;
}

.medium-editor-toolbar-anchor-preview {
  background: #242424;
  border-radius: 5px;
  color: #fff;
}

.medium-editor-placeholder:after {
  color: #b3b3b1;
}
</style>
