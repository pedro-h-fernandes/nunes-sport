<template>
    <!-- <section v-if="produtos.length <= 0">
        <span>Nenhum produto cadastrado</span>
    </section> -->
    <section class="container-fluid table-responsive">
        <table class="table table-striped table-hover">
            <thead>
                <tr>
                    <th scope="col">Código do produto</th>
                    <th scope="col">Nome</th>
                    <th scope="col">Descrição</th>
                    <th scope="col">Preço</th>
                    <th style="text-align: center;" scope="col">Ações</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="produto in produtos" :key="produto.id">
                    <th scope="row">{{ produto.id }}</th>
                    <td>{{ produto.nome }}</td>
                    <td>{{ produto.descricao }}</td>
                    <td>{{ produto.preco }}</td>
                    <td>
                        <div id="botoes" class="d-flex">
                            <ModalEdicao :produtos="produtos" :idComSimbolo="retornaTextoIdComSimbolo(produto.id)" />
                            <button type="button" class="btn m-3 btn-danger" @click="deleteProduto(produto.id)">
                                Deletar</button>
                        </div>
                    </td>
                </tr>

            </tbody>
        </table>
    </section>
</template>

<script setup>
import { onMounted, onUpdated, ref } from 'vue'
import ModalEdicao from '@/components/ModalEdicao.vue'

onMounted(async () => {
    await getProdutos()
})

onUpdated(async () => {
    await getProdutos()
})

const produtos = ref(null)

const getProdutos = async () => {
    const req = await fetch('http://localhost:3000/produtos')
    const data = await req.json()
    produtos.value = data

}
const retornaTextoIdComSimbolo = (id) => {
    return `#staticBackdrop_${id}`
}

const deleteProduto = async (id) => {
    const req = await fetch(`http://localhost:3000/produtos/${id}`, {
        method: "DELETE" //este modo de fazer funciona por conta da lib json serve onde esta sendo feito o bakend
    })

    const res = await req.json()

    getProdutos()
}
</script>
<style scoped>
span {
    color: #fff;
}
#botoes {
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
}

table {
    width: 100%;
}
</style>