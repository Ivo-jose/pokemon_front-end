<template>
    <div class="mt-6 p-6">
        <h1 class="title is-1">{{ index }} - {{ upper(name) }}</h1>
        <hr>
        <div class="card card-shadow card-radius">
        <div class="card-image has-background-primary-light">
            <div id="imagem">
                <figure>
                    <img :src="pokemon.front" alt="Placeholder image">
                </figure>
            </div>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-left has-background-primary-light">
                    <figure class="image is-96x96">
                    <img :src="pokemon.back" alt="Placeholder image">
                    </figure>
                </div>
                <div class="media-content">
                    <p class="title is-4">{{ upper(name) }}</p>
                    <p class="subtitle is-4 mb-1"><strong>Tipo:</strong> {{ pokemon.type }}</p>
                    <p class="subtitle is-6"><strong>Url:</strong> {{ url }}</p>
                </div>
            </div>

            <div class="content">
                
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
                console.log(this.pokemon);
            })
        },
        data() {
            return {
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
            }
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
</style>