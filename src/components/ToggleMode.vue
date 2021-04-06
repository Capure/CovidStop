<template>
    <div class="center">
        <div class="wrapper">
            <button @click="toggleBtn(true)" :class="['btn', 'btn-left', global ? 'btn-active' : null]">Global</button>
            <button @click="toggleBtn(false)" :class="['btn', 'btn-right', global ? null : 'btn-active']">Poland</button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            global: true
        }
    },
    methods: {
        toggleBtn(newValue) {
            this.global = newValue;
            this.$emit('toggled', this.global);
        }
    }
}
</script>

<style scoped>
.wrapper {
    width: 300px;
    height: 50px;
}

.center {
    width: 100%;
    display: flex;
    justify-content: center;
}

.btn {
    box-sizing: border-box;
    border: 1px solid white;
    height: 100%;
    width: 50%;
    border-radius: 0px;
    background-color: black;
    color: white;
    font-size: 18px;
    font-family: inherit;
    cursor: pointer;
    user-select: none;
}

.btn-left {
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
}

.btn-right {
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
}

.btn-active {
    background-color: #FFF;
    color: black;
}
</style>