<template>
    <img class="notation" v-if="mutableInput !== ''" :src="getImgUrl()" />
</template>

<script>
export default {
    name: 'InputImage',
    props: {
        input: {
            type: String,
            required: true,
        },
    },
    data() {
        return {
            mutableInput: this.input,
            imgUrl: '',
        }
    },
    methods: {
        resetMutableInput() {
            this.mutableInput = ''
        },
        getImgUrl() {
            try {
                return require('../assets/' + this.mutableInput + '.png')
            } catch (e) {
                this.resetMutableInput()
                return ''
            }
        },
    },
    computed: {
        
    },

    watch: {
        input(newVal) {
            this.mutableInput = newVal
            this.imgUrl = this.getImgUrl()
        },
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 40px 0 0;
}
ul {
    list-style-type: none;
    padding: 0;
}
li {
    display: inline-block;
    margin: 0 10px;
}
a {
    color: #42b983;
}

.input-box {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    padding: 20px;
}

.notation {
    width: 55px;
    height: 55px;
}
</style>
