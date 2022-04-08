<template>
    <div class="background"></div>
    <div class="foreground" id="mainContainer">
        <h1>Tekken Notation Converter</h1>

        <input v-model="textInput" placeholder="Write input here (e.g f n d df 2)" />
        <button class="button" @click="createImageFromInputs()">Convert notation to image file</button>

        <div v-if="textInput.length > 0" class="input-box" id="inputBox">
            <InputImage v-for="(input, index) in convertTextInputToArray" :key="index" :input="input.toLowerCase()" />
        </div>
    </div>
</template>

<script>
import InputImage from './InputImage.vue'

import html2canvas from 'html2canvas'

export default {
    name: 'TextInterface',
    props: {
        msg: String,
    },
    components: {
        InputImage,
    },
    data: function () {
        return {
            textInput: '',
        }
    },
    computed: {
        convertTextInputToArray() {
            // `this` points to the component instance
            return this.textInput.split(' ')
        },
    },
    methods: {
        createImageFromInputs() {
            let mainContainer = document.getElementById('mainContainer')
            html2canvas(document.querySelector('#inputBox'), { backgroundColor: null, scale: 4 }).then((canvas) => {
                let pngImage = this.convertCanvasToImage(canvas)
                console.log(pngImage)

                if (document.getElementById('image')) {
                    mainContainer.removeChild(document.getElementById('image'))
                }

                let link = document.createElement('a')
                console.log(pngImage)
                link.href = pngImage.src
                link.download = 'TekkenNotation.png'
                document.body.appendChild(link)
                link.click()
                document.body.removeChild(link)
            })
        },
        convertCanvasToImage(canvas) {
            let image = new Image()
            image.src = canvas.toDataURL()
            image.id = 'image'
            return image
        },
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Quicksand&display=swap');
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

* {
    font-family: 'Quicksand';
    padding: 0;
    margin: 0;
    color: #fff;
}

h1 {
    font-weight: 200;
    font-size: 45px;
    margin-top: 10vh;
    text-shadow: 1px 1px 9px #ffffff33;
    font-variant: small-caps;
}

.input-box {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    padding: 20px;
}

.background {

    background-image: url(../assets/background.jpg);
    background-size: cover;
    filter:opacity(0.9);
    background-position: center;
    background-repeat: no-repeat;
    height: 100vh;
    width: 100vw;
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.foreground {
    background-position: center;
    background-repeat: no-repeat;
    height: 100vh;
    width: 100vw;
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: center;
}

input {
    margin-top: 10vh;
    background-color: #00000044;
    color: #fff;
    border: none;
    font-size: 34px;
    width: 80vw;
    text-align: center;
    padding: 10px;
    transition: transform 0.3s ease;
    box-shadow: 2px 2px 8px #00000066;
}

input:focus,
textarea:focus,
select:focus {
    outline: none;
}

input:hover {
    transform: scale(1.05);
}

input:focus {
    transform: scale(1.05);
}

* {
}

canvas {
    position: absolute;
    z-index: 999;
}

.button {
    background-color: #00000066;
    border: none;
    padding: 10px;
    margin: 10px;
    box-shadow: 2px 2px 8px #00000044;
    font-size: 18px;
    transition: transform 0.3s ease, color 0.3s ease;
    color: #ffffffbb;
}

.button:hover {
    cursor: pointer;
    transform: scale(1.05);
    color: #ffffffff;
}
</style>
