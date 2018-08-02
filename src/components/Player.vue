<template>
    <div>
        <span v-hide v-html="welcomeMessage"></span>
        <form v-hide>
            <input name="player" placeholder="Entrez votre nom de joueur" v-border:red />
            <button  type="submit" v-border:green>Jouer</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'player',
    created: function() {
        this.player = 'Benjamin'
        this.playerClass = this.player ? 'player' : 'playerForm'
        this.welcomeMessage = this.player ? `Bonjour <span class="player">${this.player}</span> !` : ''
    },
    directives: {
        border: function(el, binding) {
            el.style.borderColor = binding.arg
        },
        hide: function(el, binding, vnode) {
            let isForm = vnode.tag == 'form'
            let player = vnode.context.player
            if (isForm) {
                el.style.display = player ? 'none' : 'block'
            } else {
                el.style.display = player ? 'block' : 'none'
            }
        }
    }
}
</script>

<style scoped>
</style>