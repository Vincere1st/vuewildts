<template>
    <div class="home">
        <div class="nav">
            <span v-for="(tag, key) in tags" :key="key">
                <input type="checkbox" v-model="tagsChecked[key]"><label
                    :class="{ [tag.color]: true, striketrought: !tagsChecked[key] }">{{ tag.title }}</label>
            </span>
        </div>
        <affectations :columns="columns" :tickets="ticketsWithTagsSelected()" :tags="tags"></affectations>
    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import data from '../data';
    import Affectations from "@/components/Affectations.vue";
    import index from "vue-router/src/index";

    @Component({
            components: {
                Affectations
            },
        },
    )

    export default class Home extends Vue {
        dreamTeam = data.dreamTeam
        columns = data.columns
        tags = data.tags
        tickets = data.tickets
        tagsChecked: any = {}

        created() {
            this.tagsChecked = this.buildDefaultTagsCheck()
        }

        beforeUpdate() {
            this.ticketsWithTagsSelected()
        }

        buildDefaultTagsCheck() {
            let defaultTagChecked: any = {}
            for (const tag in this.tags) {
                defaultTagChecked[tag] = true
            }
            return defaultTagChecked
        }

        tagsSelected() {
            const tagsSelected = []
            for (const tags in this.tagsChecked) {
                if (this.tagsChecked[tags] === true) {
                    tagsSelected.push(parseInt(tags))
                }
            }
            return tagsSelected
        }

        ticketsWithTagsSelected() {
            // return Object.values(this.tickets).filter((ticket) => {
            //     for (const tag of ticket.tags) {
            //         if (this.tagsSelected().includes(tag)){
            //             return true
            //         }
            //         return false
            //     }
            // })
            let ticketWithIndex = this.tickets
                for (const index in ticketWithIndex) {
                    ticketWithIndex[index].index = parseInt(index)
                }

            let ticketsFilter = []
                for (const ticket of Object.values(ticketWithIndex)) {
                    for (const tag of ticket.tags) {
                        console.log(tag +' tag')
                        if (this.tagsSelected().includes(tag)) {
                            console.log(ticket.index + ' index')
                            ticketsFilter.push(ticket)
                        }
                    }
                }


            // for (const tag of this.tagsSelected()) {
            //     console.log(tag)
            //     for (const ticket of Object.values(this.tickets)) {
            //         console.log(ticket.tags)
            //         if (ticket.tags.includes(tag)){
            //             ticketsFilter.push(ticket)
            //         }
            //     }
            // }
            return ticketsFilter
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
