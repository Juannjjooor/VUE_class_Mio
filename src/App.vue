<template>
    <section>
        <h2>Renderización de variables</h2>
        {{message}} <div v-html="message"></div>
        <h2>Renderizado condicional</h2>
        <h1 v-if="isVisible">Cu cu trá</h1>
        <h2>Bucles</h2>
        <ul>
            <li v-for="(item,index) in saludos">
                {{index + 1}} - {{item.text}}
            </li>
        </ul>
        <h2>Uso de referencias</h2>
        <div ref="miDiv">XXX</div>
        <h2>Doble binding (v-model)</h2>
        
        <label>
            <input v-model="isActive" type="checkbox">Activo
        </label>

        <template v-if="isActive">
            <h3>Está activo</h3>
            <h4>está activo</h4>
        </template>
        <template v-else>
            <h3>Está inactivo</h3>
            <h4>Está inactivo</h4>
        </template>


        <h2>Uso de métodos</h2>
        <button v-bind:disabled="!isActive" v-on:click="upper">Pasar a mayúsculas</button>
        <h2>Variables computadas</h2>
        <input type="text" v-model="nombre" placeholder="Nombre">
        <input type="text" v-model="apellidos" placeholder="Apellidos">
        <br>
        {{nombreCompleto}}
        <hr>
        <label>
        <input type="checkbox" v-model="onlyAlcohol">Mostrar solo alcoholicas
        </label>
        <input type="text" v-model="search"
        placeholder="Buscar...">
        <ul>
            <li v-for="item in drinksFiltered">
                {{item.name}}
            </li>
        </ul>
        <h2>Manipulación de clases</h2>
        <label><input type="checkbox" v-model="showRed">Mostrar en Rojo</label>
        <h4 :class="{'rojo': showRed}">{{miTexto}}</h4>
        <h4 :class="objetoClass">{{miTexto}}</h4>

        <select v-model="size">
            <option value="10">10px</option>
            <option value="15">15px</option>
            <option value="20">20px</option>
        </select>
        <p :style="{fontSize: size + 'px'}">Hola mundo</p>

        <h2>Ocultando con v-show</h2>
        <label>
            <input type="checkbox" v-model="showHello">Mostrar Hello
        </label>
        <h4 v-show="showHello">Hola!</h4>

        <h2>Recorrer un objeto</h2>
        <div v-for="(item, index) of persona">
            {{index}} - {{item}}
            <template v-if="index==='hobbies'">
                <ul>
                    <li v-for="hobby in item">{{hobby}}</li>
                </ul>
            </template>
        </div>
        <ul>
            <li v-for="n in 10">{{n}}</li>
        </ul>
        <ul>
            <li v-for="n in [1,2,3]">{{n+100}}</li>
        </ul>
        <ul>
            <template v-for="item in drinks">
                <li>{{ item.name }}</li>
                <li class="divider" role="presentation">-----</li>
            </template>
        </ul>

        <div>
            <a href="#" @click.prevent="counter++">Suma 1</a>
            <p>Has pulsado {{counter}} veces</p>
        </div>

        <h2>Eventos de teclas</h2>
        <input @keydown.once="pulsado" @keyup.once="soltado">

        <h3>Modificadores en v-model</h3>
        <input type="text" v-model.number="edad">
        {{ typeof edad}}
        <input type="text" v-model.trim="email">
        <div style="background-color:black;color:white">{{email}}</div>


    </section>
</template>



<script>

    export default {
        name: "MiComponente",
        data() {
            return {
                email: "juanjosegonzalezsevilla@gmail.com",
                edad: 10,
                counter: 0,
                showHello: true,
                size: 10,
                miTexto: "Hola!",
                showRed: false,
                search: "",
                onlyAlcohol: false,
                nombre: "",
                apellidos: "",
                message: "<h1>Hola mundo</h1>",
                isVisible: true,
                isActive: false,
                saludos: [
                    { text: 'Hola' },
                    { text: 'Adios' }
                ],
                drinks : [
                    {name: 'cola', alcohol: false},
                    {name: 'lemonade', alcohol: false},
                    {name: 'cubalibre', alcohol: true},
                    {name: 'coffee', alcohol: false},
                    {name: 'mojito', alcohol: true},
                    {name: 'water', alcohol: false},
                    {name: 'beer', alcohol: true}
                ],
                persona: {
                    name: "Juanjo",
                    lastname: "González",
                    hobbies: ["estudiar inglés", "surf", "programación"]
                }

            
            }
        },
        methods: {
            upper(){
                this.$refs.miDiv.innerText ="Que pasa"
                this.message = this.message.toUpperCase()
            },
            pulsado() {
                this.time = new Date ()
            },
            soltado(event){
                const now = new Date()
                const duration = (now - this.time)/1000
                console.log(`Has pulsado ${event.key} durante ${duration} segundos`)
            }

        },

        computed: {
            objetoClass() {
                return {
                    rojo: this.showRed
                }
            },


            drinksFiltered(){
                return this.drinks.filter(item => {
                    return item.alcohol === this.onlyAlcohol && item.name.includes(this.search)
                })
            },
            nombreCompleto() {
                return this.nombre + " " + this.apellidos
            },
            



        }
    }

    

</script>


<style scoped>
    .rojo {
        color: red;
    }

</style>

d