<template>
<div class="modal" :class="{'is-active' : ativo}">
    <div class="modal-background"></div>
        <div class="modal-card">
            <header class="modal-card-head">
                <p class="modal-card-title">{{titulo}}</p>
                <button @click="$emit('close')" class="delete" aria-label="close"></button>
            </header>
            <section class="modal-card-body">
               <slot name="conteudo"></slot>
            </section>
            <footer class="modal-card-foot">
                <slot name="footer"></slot>
                <button class="button is-success" @click="$emit('salvar')">Salvar</button>
                <button class="button" @click="$emit('close')">Cancel</button>
            </footer>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        ativo: {
            type: Boolean,
            required: true
        },
        titulo: {
            type: String,
            required: true
        }
    }

}
</script>

<style>

</style>