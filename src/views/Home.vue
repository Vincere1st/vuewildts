<template>
    <div class="home">
        <div class="nav">
            <span v-for="(tag, key) in tags" :key="key">
                <input type="checkbox" v-model="tagsChecked[key]"><label :class="{ [tag.color]: true, striketrought: !tagsChecked[key] }">{{ tag.title }}</label>
            </span>
        </div>
        <affectations :columns="columns" :tickets="tickets" :tags="tags" :showtickets="showTickets"></affectations>
    </div>
</template>

<script lang="ts">
import {Component, Vue} from 'vue-property-decorator';
import data from '../data';
import Affectations from "@/components/Affectations.vue";

@Component({
    components: {
        Affectations
    },
})
export default class Home extends Vue {
    dreamTeam = data.dreamTeam
    columns = data.columns
    tags = data.tags
    tickets = data.tickets

    tagsChecked:any = {}

    created () {
        this.tagsChecked = this.buildDefaultTagsCheck()
    }

    buildDefaultTagsCheck() {
        let defaultTagChecked: any = {}
        for (const tag in this.tags) {
            defaultTagChecked[tag] = true
            Object.assign(defaultTagChecked, {tag: true})
        }
        return defaultTagChecked
    }

    showTickets() {
        console.log('tata')
        // for (const tag in this.tags){
        //     if (this.buildDefaultTagsCheck[tag] === true) {
        //         console.log('toto')
        //     }
        // }
    }
}
</script>

<style lang="scss">
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

    .striketrought {
        text-decoration: line-through;
    }
</style>
