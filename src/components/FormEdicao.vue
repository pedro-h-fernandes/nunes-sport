<template>
    <main>
        <form @submit.prevent="editarProduto">
            <div class="mb-3">
                <label for="exampleInputNome1" class="form-label">Nome</label>
                <input type="text" :value="nome" @input="nome = $event.target.value" required class="form-control"
                    id="exampleInputNome1" aria-describedby="NomeHelp">
            </div>
            <div class="mb-3">
                <label for="exampleFormControlTextarea1" class="form-label">Descrição do produto</label>
                <textarea class="form-control" :value="descricao" @input="descricao = $event.target.value" required
                    id="exampleFormControlTextarea1" rows="3"></textarea>
            </div>
            <div class="input-group mb-3">
                <span class="input-group-text">R$</span>
                <input type="text" class="form-control" :value="preco" @input="preco = $event.target.value"
                    aria-label="preço em real">
            </div>

            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Fechar</button>
                <button type="submit" class="btn btn-primary">Salvar</button>
            </div>
        </form>
    </main>
</template>
<script setup >
import { ref, defineProps, onBeforeMount } from 'vue'

onBeforeMount(async () => {
    await getProdutosPorId(props.produtoId)
})

const nome = ref(null)
const descricao = ref(null)
const preco = ref(null)

const props = defineProps(['produtoId'])

const getProdutosPorId = async (id) => {
    JSON.stringify(id)
    const req = await fetch(`http://localhost:3000/produtos/${id}`)

    const produto = await req.json()
    nome.value = produto.nome
    descricao.value = produto.descricao
    preco.value = produto.preco
}


const editarProduto = async () => {
    const data = {
        nome: nome.value,
        descricao: descricao.value,
        preco: preco.value
    };

    const dataJson = JSON.stringify(data);

    const req = await fetch(`http://localhost:3000/produtos/${props.produtoId}`, {
        method: 'PUT',
        headers: { "Content-Type": "application/json" },
        body: dataJson,
    });

    const res = await req.json();
};
</script>
<style lang="">
    
</style>