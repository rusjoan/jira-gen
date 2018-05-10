<template>
  <div class="pdf-page">
    <div class="task" :class="{'bug': task.bug === 1}" v-for="(task, idx) in tasks" :key="idx">
      <div class="header">
        <span class="number">
          {{ task.number }}
          <span>{{ task.price }}</span>
        </span>
        <span class="title">{{ task.title }}</span>
      </div>
      <div class="body">
        {{ task.description }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['tasks'],
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" rel="stylesheet/sass">
  $border-color: rgba(0,0,0,.2);
  .pdf-page {
    size: A4;
    width: 209mm;
    height: 296mm;
    box-shadow: 1px 1px 10px rgba(0,0,0,.4);
    margin: 10px auto 30px auto;
    vertical-align: top;
    padding: 2cm;
  }
  @media print {
    .pdf-page {
      box-shadow: none;
      margin: 0;
    }
  }
  .task {
    color: black;
    width: 76mm;
    height: 76mm;
    font-size: 6mm;
    //border: .5mm solid $border-color;
    /*border-bottom: .1mm solid gray;*/
    position: relative;
    display: inline-flex;
    flex-direction: column;
    font-family: 'Open Sans', sans-serif;
    margin: 0 4mm 4mm 4mm;
    overflow: hidden;
    position: relative;
    //background: #f5ff75 !important;
    &:before {
      display: block;
      content: ' ';
      position: absolute;
      width: 100%;
      height: 10mm;
      border: .4mm solid gray;
      border-bottom: 0;
    }
    &.bug {
      background: #ffc7c7 !important;
    }
    .header, .body, .footer {
    }
    .header {
      padding: 4mm 4mm 2mm 4mm;
      border-bottom: .5mm solid gray;
      font-size: 4mm;
      line-height: 4mm;
      .number {
        font-weight: bold;
        display: block;
        font-size: 10mm;
        line-height: 8mm;
        min-height: 6mm;
        span {
          float: right;
          font-weight: 300;
          color: rgba(0,0,0,.5)
        }
      }
    }
    .body {
      padding: 2mm 4mm 2mm 4mm;
      flex: 1;
      font-size: 7.4mm;
      line-height: 1em;
      text-overflow: ellipsis;
      font-weight: 300;
    }
    .footer {
      font-size: .6em;
      position: absolute;
      /*bottom: .5mm;*/
      /*right: .5mm;*/
      bottom: 0;
      width: 100%;
      height: 8mm;
      /*font-weight: bold;*/
      text-align: right;
      background: linear-gradient(rgba(255,255,255,0), rgba(255,255,255,.8) 50%) !important;
    }
  }
  @page {
    size: A4;
    /*margin: .2cm;*/
  }
</style>
