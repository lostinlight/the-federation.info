<template>
    <table id="nodes-table">
        <thead>
            <tr>
                <th>Software</th>
                <th>Name</th>
                <th class="version-column">Version</th>
                <th>Open signups</th>
                <th>Total users</th>
                <th>Active users half year</th>
                <th>Active users monthly</th>
                <th>Local posts</th>
                <th>Local comments</th>
                <th>Services</th>
                <th>Country</th>
            </tr>
        </thead>
        <tbody>
            <NodesTableRow
                v-for="node in nodes"
                :node="node"
                :stats="statsForNode(node.id)"
                :key="node.id"
            />
        </tbody>
    </table>
</template>

<script>
import NodesTableRow from "./NodesTableRow"

export default {
    name: "NodesTable",
    components: {NodesTableRow},
    props: {
        nodes: {
            type: Array,
            default: () => [],
        },
        stats: {
            type: Object,
            default: () => {},
        },
    },
    mounted() {
        // eslint-disable-next-line no-undef
        makeSortable(document.getElementById("nodes-table"))
    },
    methods: {
        statsForNode(nodeId) {
            if (this.stats[nodeId] === undefined) {
                return {
                    usersTotal: 0,
                    usersHalfYear: 0,
                    usersMonthly: 0,
                    localPosts: 0,
                    localComments: 0,
                }
            }
            return this.stats[nodeId]
        },
    },
}
</script>

<style scoped>
    .version-column {
        max-width: 150px;
        overflow: hidden;
    }
</style>
