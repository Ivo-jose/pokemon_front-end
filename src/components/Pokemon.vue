<template>
    <div id="caixa" class="mt-6 p-6">
        <h1 class="title is-3 has-text-danger">{{ index }} - {{ upper(name) }}</h1>
        <hr>
        <div class="card card-shadow card-radius">
        <div class="card-image has-background-primary-light">
            <div id="imagem">
                <figure>
                    <img :src="currentImgFront" alt="Placeholder image">
                </figure>
            </div>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-left has-background-primary-light">
                    <figure class="image is-96x96">
                    <img :src="currentImgBack" alt="Placeholder image">
                    </figure>
                </div>
                <div class="media-content">
                    <p class="title is-4">{{ upper(name) }}</p>
                    <p class="subtitle is-4 mb-1"><strong>Tipo principal:</strong> {{ pokemon.type }}</p>
                    <p class="subtitle is-6"><strong>Url:</strong> {{ url }}</p>
                </div>
            </div>

            <div class="content">
                <button @click="mudarSprite" class="button is-danger is-rounded">Inverter imagem</button>
            </div>
        </div>
        <hr>
</div>

    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        created: function() {
            axios.get(this.url).then(res => {
                this.pokemon.type = res.data.types[0].type.name;
                this.pokemon.front = res.data.sprites.front_default;
                this.pokemon.back = res.data.sprites.back_default; 
                this.currentImgFront = this.pokemon.front;
                this.currentImgBack = this.pokemon.back
                console.log(this.pokemon);
            })
        },
        data() {
            return {
                isFront: true,
                isBack: true,
                currentImgFront: "",
                currentImgBack:"",
                pokemon: {
                    type: '',
                    front: '',
                    back: '',
                    abilities: []
                }
            }
        },
        props: {
            index: Number,
            name: String,
            url: String
        },

        methods: {
            upper: function (value) {
                return `${value[0].toUpperCase()}${value.slice(1)}`;
            },

            mudarSprite: function() {
                if(this.isFront && this.isBack) {
                    this.isFront = false;
                    this.isBack = false;
                    this.currentImgFront = this.pokemon.back;
                    this.currentImgBack = this.pokemon.front;
                }
                else {
                    this.isFront = true;
                    this.isBack = true;
                    this.currentImgFront = this.pokemon.front;
                    this.currentImgBack = this.pokemon.back;
                }
            },  
        }
    }
</script>

<style>
img {
    height: 300px;
    width: 300px;
    display: flex;
    justify-content: center;
}

#imagem {
    margin: 0 auto;
    height: 310px;
    width: 310px;
    padding: 5px;
}

button:hover {
    font-weight: bold;
    box-shadow: 4px 4px 6px rgb(42, 42, 42);
}
</style>