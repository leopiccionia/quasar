<template>
  <div>
    <div class="layout-padding">

      {{ inputModelRgb }} <q-btn @click="inputModelRgb = null" label="Clear" />
      <p>Immediate</p>
      <q-color v-model="inputModelRgb" stack-label="simple" />
      <q-color v-model="inputModelRgb" clearable stack-label="clearable" />
      <q-color v-model="inputModelRgb" default-value="#ccc" stack-label="default-value" />
      <q-color v-model="inputModelRgb" default-value="#ccc" clearable stack-label="default-value, clearable" />
      <p>Lazy</p>
      <q-color :value="inputModelRgb" @change="val => inputModelRgb = val" stack-label="simple" />
      <q-color :value="inputModelRgb" @change="val => inputModelRgb = val" clearable stack-label="clearable" />
      <q-color :value="inputModelRgb" @change="val => inputModelRgb = val" default-value="#ccc" stack-label="default-value" />
      <q-color :value="inputModelRgb" @change="val => inputModelRgb = val" default-value="#ccc" clearable stack-label="default-value, clearable" />

      <br><br>
      <q-btn color="primary" label="Set to yellow" @click="setToYellow"/>

      <div class="row gutter-md" style="width: 550px">
        <div class="col-6">
          <q-color-picker v-model="modelHex" @input="value => log('@input', value)" @change="value => log('@change', value)" />
          <div class="inline-block text-white" style="text-shadow: black 0px 0px 7px; padding: 10px" :style="{ backgroundColor: this.modelHex }">
            <pre>Hex: {{modelHex}}</pre>
          </div>
        </div>
        <div class="col-6">
          <q-color-picker v-model="modelHexa" />
          <div class="inline-block text-white" style="text-shadow: black 0px 0px 7px; padding: 10px" :style="{ backgroundColor: this.modelHexa }">
            <pre>Hexa: {{modelHexa}}</pre>
          </div>
        </div>
        <div class="col-6">
          <q-color-picker v-model="modelRgb" />
          <div class="inline-block text-white" style="text-shadow: black 0px 0px 7px; padding: 10px" :style="{ backgroundColor: rgb(this.modelRgb) }">
            <pre>RGB: {{modelRgb}}</pre>
          </div>
        </div>
        <div class="col-6">
          <q-color-picker v-model="modelRgba" />
          <div class="inline-block text-white" style="text-shadow: black 0px 0px 7px; padding: 10px" :style="{ backgroundColor: rgb(this.modelRgba) }">
            <pre>RGBA: {{modelRgba}}</pre>
          </div>
        </div>
      </div>

      <h4>Lazy</h4>
      <div class="row gutter-md" style="width: 550px">
        <div class="col-6">
          <q-color-picker :value="modelHex" @change="model => { modelHex = model; log('@change', model) }" @input="value => log('@input', value)" />
          <div class="inline-block text-white" style="text-shadow: black 0px 0px 7px; padding: 10px" :style="{ backgroundColor: this.modelHex }">
            <pre>Hex: {{modelHex}}</pre>
          </div>
        </div>
        <div class="col-6">
          <q-color-picker :value="modelHexa" @change="model => { modelHexa = model }" />
          <div class="inline-block text-white" style="text-shadow: black 0px 0px 7px; padding: 10px" :style="{ backgroundColor: this.modelHexa }">
            <pre>Hexa: {{modelHexa}}</pre>
          </div>
        </div>
      </div>

      <h4>Input</h4>
      <q-color v-model="inputModelHex" clearable default-value="#ffffff" @input="value => log('@input', value)" @change="value => log('@change', value)" />
      <q-color v-model="inputModelHex" inverted readonly float-label="Readonly" />
      <q-color v-model="inputModelRgb" float-label="RGB" />
      <q-color v-model="inputModelRgb" inverted disable float-label="Disable" />

      <h4>Lazy Input</h4>
      <q-color :value="inputModelHex" @change="val => { inputModelHex = val; log('@change', val)}" @input="value => log('@input', value)" clearable />

      <h4>Type: <small>{{modelVar}}</small></h4>
      <q-color v-model="modelVar" clearable @input="value => log('@input', value)" @change="value => log('@change', value)" stack-label="Type 'auto'" type="auto" />
      <q-color v-model="modelVar" clearable @input="value => log('@input', value)" @change="value => log('@change', value)" stack-label="Type 'hexa'" type="hexa" />
      <q-color v-model="modelVar" clearable @input="value => log('@input', value)" @change="value => log('@change', value)" stack-label="Type 'hex'" type="hex" />
      <q-color v-model="modelVar" clearable @input="value => log('@input', value)" @change="value => log('@change', value)" stack-label="Type 'rgba'" type="rgba" />
      <q-color v-model="modelVar" clearable @input="value => log('@input', value)" @change="value => log('@change', value)" stack-label="Type 'rgb'" type="rgb" />

      <h4>Explicit Popover or Modal</h4>
      <q-color         v-model="inputModelRgb" float-label="RGB Default" />
      <q-color popover v-model="inputModelRgb" float-label="RGB Popover" />
      <q-color modal   v-model="inputModelRgb" float-label="RGB Modal" />
      <q-color modal   v-model="inputModelRgb" float-label="RGB Modal Readonly " readonly  />

      <h4>Readonly</h4>
      <div class="row gutter-md" style="width: 550px">
        <div class="col-6">
          <q-color-picker v-model="modelHex" readonly />
        </div>
        <div class="col-6">
          <q-color-picker v-model="modelHexa" readonly />
        </div>
        <div class="col-6">
          <q-color-picker v-model="modelRgb"  readonly />
        </div>
        <div class="col-6">
          <q-color-picker v-model="modelRgba" readonly />
        </div>
      </div>

      <h4>Disable</h4>
      <div class="row gutter-md" style="width: 550px">
        <div class="col-6">
          <q-color-picker v-model="modelHex" disable />
        </div>
        <div class="col-6">
          <q-color-picker v-model="modelHexa" disable />
        </div>
        <div class="col-6">
          <q-color-picker v-model="modelRgb"  disable />
        </div>
        <div class="col-6">
          <q-color-picker v-model="modelRgba" disable />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      modelHex: '#FF00FF',
      modelHexa: '#FF00FFCC',
      modelRgb: { r: 0, g: 0, b: 0 },
      modelRgba: { r: 255, g: 0, b: 255, a: 100 },
      modelVar: '#FF00FF',
      inputModelHex: null,
      inputModelRgb: { r: 245, g: 20, b: 150 }
    }
  },
  methods: {
    rgb (color) {
      return `rgb${color.a !== void 0 ? 'a' : ''}(${color.r},${color.g},${color.b}${color.a !== void 0 ? `,${color.a / 100}` : ''})`
    },
    setToYellow () {
      this.modelHex = '#FFFF00'
      this.modelHexa = '#FFFF00FF'
      this.modelRgb = {r: 255, g: 255, b: 0}
      this.modelRgba = {r: 255, g: 255, b: 0, a: 100}
    },
    log (name, data) {
      console.log(name, JSON.stringify(data))
    }
  }
}
</script>
