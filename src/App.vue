<template>
  <div id="app">
    <div class="left">
      <hot-table :root="root" :settings="hotSettings"></hot-table>
    </div>
    <div class="right">
      <template v-for="(chunk, idx) in chunks">
        <Page :tasks="chunk" :key="idx" />
      </template>
    </div>
  </div>
</template>

<script>
import Page from './components/Page'
import HotTable from '@handsontable/vue'

const tasks = require('../static/tasks')

export default {
  name: 'App',
  data: () => ({
    // tasks,
    root: 'test-hot',
    hotSettings: {
      columns: [
        {data: 'number', type: 'text', width: 80},
        {data: 'title', type: 'text', width: 200},
        {data: 'description', type: 'text', width: 400},
        {data: 'price', type: 'text', width: 40},
        {data: 'bug', type: 'numeric', width: 40},
      ],
      minRows: 1,
      colHeaders: ['Number', 'Title', 'Description', 'Price', 'Bug?'],
      width: '100%',
      // data: tasks,
      data: [
        {
          "number": "",
          "title": "Заголовок",
          "description": "Описание",
          "price": "",
          "bug": undefined,
        },
      ],
    }
  }),
  computed: {
    tasks () {
      return this.hotSettings.data.filter(t => t.description && t.description.length > 0);
    },
    chunks () {
      const chunkSize = 6;
      return Array(Math.ceil(this.tasks.length / chunkSize)).fill(0).map((_, idx) => {
        return this.tasks.slice(idx * chunkSize, (idx+1) * chunkSize);
      })
    }
  },
  components: {
    Page,
    HotTable,
  },
}
</script>

<style src="../node_modules/handsontable/dist/handsontable.full.css"></style>
<style lang="scss" rel="stylesheet/sass">
  body {
    background: #fafafa;
    padding: 1em;
  }
  #app {
    display: flex;
    .left, .right {
      flex: 1 100%;
      min-width: 400px;
    }
    .left {
      overflow: hidden;
    }
    textarea {
      height: 30em;
    }
  }
  @media print {
    body {
      padding: 0;
      -webkit-print-color-adjust: exact;

    }
    .left {
      display: none;
    }
  }
</style>
