

<script>
    import Vue from 'vue'
    export default {
        data () {
            return {
                new: '',
                contacts: []
                // contacts: ['(11) 2423-2324', '(11) 4356-6567', '(31) 3976-3345']
            }
        },
        methods: {
            handler (index, contact) {
                if (contact == '') {
                    window.console.log(index)
                    this.contacts.splice(index, 1)
                    this.focusLastField()
                }
            },
            add () {
                if (this.new != '') {
                    this.contacts.push(this.new)
                    this.new = ''
                    this.focusLastField()
                }
            },
            focusLastField () {
                const lastIndex = this.contacts.length - 1
                const selector = `[data-index="${lastIndex}"]`
                Vue.nextTick(() => {
                    const field = document.querySelector(selector)
                    if (field != null) {
                        field.focus()
                    }
                })
            },
        }
    }
</script>

<template>
    <div>
        <div id="app">
            <div v-for="contact in contacts" track-by="$index">
                <input :data-index="$index" type="text" v-model="contact" @keyup="handler($index, contact)">
            </div>
            <div>
                <input type="text" v-model="new" @keyup="add" placeholder="Adicionar telefone">
            </div>
        </div>
    </div>
</template>