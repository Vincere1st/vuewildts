<template>
    <div class="body">
        <ul v-for="column in this.orderColumnsWithIndex()">
            <span class="title"> {{column.title}} </span>
            <li v-for="ticket in orderTicketsByColumns(column.index)">
                <span v-for="tag in tagFilter(ticket.tags)" :class="{[tag.color]:true}">{{tag.title}} - </span><span>{{ticket.content}}</span>
            </li>
        </ul>
    </div>
</template>

<script lang="ts">
    import {Component, Prop, Vue} from "vue-property-decorator";

    @Component
    export default class Affectations extends Vue {
        @Prop({default: null})
        readonly columns: any
        @Prop({default: null})
        readonly tickets: any
        @Prop({default: null})
        readonly tags: any

        orderColumnsWithIndex() {
            for (const index in this.columns) {
                this.columns[index].index = index
            }

            let orderedColumns = Object.values(this.columns)
            orderedColumns.sort((a, b) => (a.order - b.order))
            return orderedColumns
        }

        orderTicketsByColumns(values: any) {
            let ticketsOrdered = []
            for (const ticket of Object.values(this.tickets)) {
                if (ticket.column == values) {
                    ticketsOrdered.push(ticket)
                }
            }
            return ticketsOrdered
        }

        tagFilter(values) {
            let tagFiltered: Array = []
            for (const index in this.tags) {
                if (values.includes(parseInt(index))) {
                    tagFiltered.push(this.tags[index])
                }
            }
            return tagFiltered
        }
    }
</script>

<style lang="scss">
    .title {
        font-weight: bold;
    }
</style>