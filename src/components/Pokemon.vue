<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div id="principal">
        <div class="card">
            <div class="card-image">
                <figure>
                <img :src="currentImg" alt="Placeholder image"/>
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-4">{{ id + 1 }} - {{ upperFirstChar }}</p>
                        <p class="subtitle is-6" style="font-style: italic;"> {{ pokemon.type }} </p>
                    </div>
                </div>

                <div class="content">
                    <button class="button is-medium is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    created: function() {
        axios.get(this.url).then( res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
            console.log(this.pokemon);
        })
    },
    data(){
        return {
            currentImg: '',
            isFront: true,
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },
    props: {
        id: Number,
        name: String,
        url: String
    },
    computed: {
        upperFirstChar() {
            let newName = this.name[0].toUpperCase() + this.name.slice(1);
            return newName;
        }
    },
    methods: {
        mudarSprite(){
            if (this.isFront) {
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            } else {
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style>
    #principal {
        margin-top: 3%;
    }
</style>