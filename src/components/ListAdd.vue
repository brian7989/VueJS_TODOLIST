<template>
    <div>
        <v-textarea
            outline
            v-model="memo"
            label="Enter Todo"
            value=""
        ></v-textarea>
        <v-btn v-if="mode === 'add'" @click="listAdd"> Add to List </v-btn>
        <v-btn v-else @click="listEdit"> Edit List </v-btn>
    </div>
</template>

<script>

import { eventBus } from "../main"
export default {
    data () {
        return {
            memo: null,
            index: null,
            mode : "add"
        }
    },
    created() {
        eventBus.$on('listEdit', (memo, index) => {
            this.memo = memo
            this.index = index
            this.mode = "edit"
        }) 
    },
    methods: {
        listAdd() {
            console.log("List added")
            if (this.memo === null) {
                alert("Todo not entered")
            } else {
                this.$emit("listAdd", this.memo)
                this.memo = null
            }
        },
        listEdit() {
            console.log("List Edited")
            if (this.memo === null) {
                alert("Todo not entered")
            } else {
                this.$emit("listEdit", this.memo, this.index)
                this.memo = null
                this.mode = "add"
            }
        }
    }
}
</script>