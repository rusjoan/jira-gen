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
    width: 210mm;
    height: 297mm;
    box-shadow: 1px 1px 10px rgba(0,0,0,.4);
    margin: 10px auto;
    vertical-align: top;
  }
  @media print {
    .pdf-page {
      box-shadow: none;
      margin: 0;
    }
  }
  .task {
    color: black;
    width: 69mm;
    height: 73mm;
    font-size: 6mm;
    border: .5mm solid $border-color;
    display: inline-flex;
    flex-direction: column;
    font-family: "PT Sans";
    margin: .5mm;
    overflow: hidden;
    position: relative;
    background: #f5ff75 !important;
    &.bug {
      background: #ffc7c7 !important;
    }
    .header, .body, .footer {
      padding: 1.6mm;
    }
    .header {
      font-family: "PT Sans Caption";
      border-bottom: .5mm solid $border-color;
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
      flex: 1;
      font-size: 6mm;
      line-height: 6mm;
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
    margin: .2cm;
  }
</style>
