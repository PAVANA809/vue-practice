<template>
  <div>
    <p>Locale</p>
    <select @change="localeChange" v-model="locale">
    <option value="US">US</option>
    <option value="DE">DE</option>
  </select>
  </div>

  <div>
    <p>Integer Format</p>
    <select v-model="IntegerFormat">
    <option value="1">#0</option>
    <option v-if="locale == 'US'" value="2">#,###</option>
    <option v-if="locale == 'DE'" value="3">#.###</option>
    </select>
  </div>

  <div>
    <p>Float Format</p>
    <select v-model="FloatFormat">
    <option v-if="locale == 'US'" value="US">#,###.00</option>
    <option v-if="locale == 'DE'" value="DE">#.###,00</option>
  </select>
  </div>

  <div v-if="locale != ''">
    <p>Thousand seperator: {{ formattedNumber }}</p>
    <p>Decimal seperator: {{ deciamlNumber }}</p>
  </div>

</template>

<script>
  export default {
  name: 'HelloWorld',
  data() {
    return {
      locale: "US",
      IntegerFormat: "1",
      FloatFormat: "US",
      number: 123456789,
      deciaml: 356.67,
    }
  },
  methods: {
    localeChange() {
      if (this.locale == 'US') {
        this.FloatFormat = "US";
      } else if (this.locale == 'DE'){
        this.FloatFormat = "DE";
      }
    }
  },
  computed: {
    formattedNumber() {
      if (this.locale == 'US' && this.IntegerFormat != '1') {
        return this.number.toLocaleString('en-US')
      } else if (this.locale == 'DE' && this.IntegerFormat != '1') {
        return this.number.toLocaleString('de-DE')
      } else {
        return this.number
      }
    },
    deciamlNumber() {
      if (this.locale == 'US') {
        return this.deciaml.toLocaleString('en-US')
      } else if (this.locale == 'DE') {
        return this.deciaml.toLocaleString('de-DE')
      } else {
        return this.deciaml
      }
    }
  }
  }
</script>

<style scoped>
  div{
    display: flex;
    align-items: flex-end;
    justify-content: center;
    margin: 10px;
  }
  p{
    margin: 0 10px;
  }
  select{
    margin: 0 10px;
  }
</style>