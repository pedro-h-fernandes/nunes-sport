<template>
    <main>
        <form @submit.prevent="cadastrarProduto">
            <div class="mb-3">
                <label for="exampleInputNome1" class="form-label">Nome</label>
                <input type="text" v-model="nome" required class="form-control" id="exampleInputNome1"
                    aria-describedby="NomeHelp">
            </div>
            <div class="mb-3">
                <label for="exampleFormControlTextarea1" class="form-label">Descrição do produto</label>
                <textarea class="form-control" v-model="descricao" id="exampleFormControlTextarea1"
                    rows="3"></textarea>
            </div>
            <div class="input-group mb-3">
                <span class="input-group-text">R$</span>
                <input type="text" class="form-control" v-model="preco" aria-label="preço em real">
            </div>

            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Fechar</button>
                <button type="submit" class="btn btn-primary">Salvar</button>
            </div>
        </form>
    </main>
</template>
<script setup >
import { ref } from 'vue'


const nome = ref(null)
const descricao = ref(null)
const preco = ref(null)

const cadastrarProduto = async () => {
    const data = {
        nome: nome.value,
        descricao: descricao.value,
        preco: preco.value
    };

    const dataJson = JSON.stringify(data);

    const req = await fetch('http://localhost:3000/produtos', {
        method: 'POST',
        headers: { "Content-Type": "application/json" },
        body: dataJson,
    });
    const res = await req.json();

    limparDados()
    alert('Salvo com sucesso')
}

const limparDados = () => {
    nome.value = "";
    descricao.value = "";
    preco.value = "";
}

</script>
<style lang="">
    
</style>