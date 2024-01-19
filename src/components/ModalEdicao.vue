<template>
    <section>
        <!-- Button trigger modal -->
        <button type="button" class="btn btn-success" data-bs-toggle="modal" :data-bs-target="idComSimbolo">
            Editar produto 
        </button>

        <!-- Modal -->
        <div v-for="produto in produtos" :key="produto.id" class="modal fade" :id="retornaTextoId(produto.id)"
            data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="staticBackdropLabelEdicao"
            aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5" id="staticBackdropLabelEdicao">Editar Produto {{ produto.id }}</h1>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <FormEdicao :produtoId="produto.id" />
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<script setup>
import {defineProps} from 'vue';
import FormEdicao from './FormEdicao.vue'


const retornaTextoId = (id) => {
    return `staticBackdrop_${id}`
}

const { idComSimbolo, produtos } = defineProps(['idComSimbolo', 'produtos'])

// const getProdutos = async () => {
//     const req = await fetch('http://localhost:3000/produtos')
//     const data = await req.json()
//     produtos.value = data
// }
</script>
<style lang="">
    
</style>