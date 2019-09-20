<template>
    <div>
        <table>
            <tr>
                <th>Celsius</th>
                <th>Fahrenheit</th>
            </tr>
            <tr v-for="t in temperatura" :key="t.celsius">
                <td><a href="#" @click="selecionar(t)">{{t.celsius}} </a></td>
                <td>{{t.fahrenheit}}</td>
            </tr>
        </table>
    </div>
</template>

<script>
export default {
    // props: ["minima"],
    props: {
        minima: {
            type: Number, //Array, Object, String
            default: 0
        },
        maxima: {
            type: Number,
            default: 100
        }
    },
    data() {
        return {
            temperatura: []
        }
    },
    mounted() {
        this.calcularTemperatura()
    },
    methods: {
        calcularTemperatura() {
            this.temperatura = []
            for (let c = this.minima; c <= this.maxima; c+=10) {                
                let f = (c * 9/5) + 32
                this.temperatura.push({
                    celsius: c,
                    fahrenheit: f
                })
            }
        },
        selecionar(temperatura) {
            console.log(temperatura)
            this.$emit('selecionar', temperatura)
        }
    },
    watch: {
        minima: function() {
            this.calcularTemperatura()
        },
        maxima: function() {
            this.calcularTemperatura()
        }
    }

}
</script>

<style>

</style>