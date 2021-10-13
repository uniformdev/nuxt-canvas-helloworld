<template>
  <fieldset>
    <legend>Component: {{ uniformData.type }}</legend>
    <h1>{{ uniformData.type }} component</h1>
    <h2>
      Parameters:
    </h2>
    <ul>
      <li v-for="parameter in uniformData.parameters" :key="parameter">
        <strong>type:</strong> {{ parameter.type }}
        <br />
        <strong>value:</strong>
        <pre>{{ parameter.value }}</pre>
      </li>
    </ul>
    <h2>
      Slots:
    </h2>
    <ul>
      <li v-for="slotName in Object.keys(uniformData.slots)" :key="slotName">
        <pre>{{ slotName }}</pre>
        <pre>{{uniformData.slots[slotName]}}</pre>
      </li>
    </ul>
  </fieldset>
</template>

<script>
export default {
  props: {
    uniformData: {
      type: Object,
      required: true
    }
  }
};
</script>
