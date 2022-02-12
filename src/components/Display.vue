<template>
    <div class="display" :class="{ mini }">
        {{ value }}
    </div>
</template>

<script>
export default {
    props: {
        value: {},
        mini: { type: Boolean}
    }  
}
</script>

<style>
.display {    
    user-select: none;
    grid-column: span 4;
    background-color: rgba(0, 0, 0, 0.568);
    display: flex;
    justify-content: flex-end;
    align-items: center;
    padding: 10px;
    font-size: 2.3em;
    overflow: hidden;
}

.display.mini {    
    font-size: 1em;
} 
</style>