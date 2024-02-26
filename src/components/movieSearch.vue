<template>
    <div>
        <v-text-field placeholder="Rechercher un film" v-model="textField">

        </v-text-field>
    </div>
</template>
<script>
import { watch } from 'vue';

export default {
    name: 'movieSearch',

    data() {
        return {
            textField: ''
        };
    },

    watch: {
        textField(newValue) {
            this.$emit('searchMovieEmit', newValue);
        }
    }
}   

</script>