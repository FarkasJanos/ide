<template>
  <div>
    <div class="row">
      <div>
        <menu-bar></menu-bar>
        <monaco-editor></monaco-editor>
      </div>
      <in-out-box></in-out-box>
    </div>
  </div>

</template>

<script>
  import inOutBox from './editor/InOutBox.vue'
  import menuBar from './editor/MenuBar.vue'
  import monacoEditor from './editor/MonacoEditor.vue'

  export default {
    name: 'editor',
    components: {
      inOutBox,
      menuBar,
      monacoEditor,
    },
    created () {
      this.$store.dispatch('loadDataFromServer')

    },
    mounted () {
      const ref = this.$route.query.ref || this.$attrs.ref
      if (ref) {
        this.$store.dispatch('firebase/startCodeSharing', ref).catch(() => {
          alert('This live code link is no longer valid')
          this.$router.push('/')
        })
      }
    }
  }
</script>

<style>
  .btn-group .btn {
    margin: 0;
    padding: 0 12px;
    height: 40px;
  }

  .headPanel {
    height: 40px !important;
    padding: 0 15px !important;
  }

  .btn span {
    font-size: 11px;
    font-weight: 700 !important;
  }

  .btn-menu {
    color: #fff !important;
    background-color: transparent;
    margin: auto 0;
  }

  .btn-menu:hover, .btn-menu:active, .btn-menu:focus {
    color: #e31d3b !important;
    box-shadow: none !important;
  }

  .btn i {
    font-size: 12px;
  }
</style>
