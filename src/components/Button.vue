<template>
  <div class="button" @click="$emit('onClick', label)" :class="{ double, triple, operation }">
      {{ label }}
  </div>
</template>

<script>
export default {
    props: {
        label: {},
        operation: { type: Boolean },
        double: { type: Boolean },
        triple: { type: Boolean }
    }
}
</script>

<style>
:root {
    --bg-button: #f0f0f0;
    --border-button: solid 1px rgb(80, 80, 80);
}

.button {
    user-select: none;
    color: rgb(49, 49, 49);
    font-size: 1.9em;
    background-color: var(--bg-button);
    border: none;
    border-right: var(--border-button);
    border-bottom: var(--border-button);
    outline: none;
}

.button:active {
    background-color: #ccc;
}

.button.double {
    grid-column: span 2;
}

.button.triple {
    grid-column: span 3;
}

.button.operation {
    background-color: #ff7f50;
}

.button.operation:active {
    background-color: #ff7f50cc;
}
</style>