<template>
    <div class="home">
        <div class="nav">
            <span v-for="tag in tags">
                <input type="checkbox" v-model="tagCkecked"><label :class={[tag.color]:true,striketrought:!tagChecked}>{{ tag.title }}</label>
            </span>
        </div>
    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import data from '../data';
    // import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src

    @Component({
        components: {
            // HelloWorld
        },
    })
    export default class Home extends Vue {
        dreamTeam = data.dreamTeam
        columns = data.columns
        tags = data.tags
        tickets = data.tickets
    }
</script>

<style lang="scss" scoped>
    .grey {
        color: darkgrey;
    }
    .green {
        color: darkgreen;
    }
    .orange {
        color: darkorange;
    }
    .red {
        color: darkred;
    }
    .purple {
        color: darkviolet;
    }
    .blue {
        color: darkblue;
    }
</style>
