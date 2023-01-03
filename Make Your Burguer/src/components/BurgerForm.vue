<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <div>
            <form  id="burger-form" @submit="creatBruger">
                <div class="input-container">
                    <label for="nome">Nome do cliente: </label>
                    <input  type="text" name="nome" id="nome" v-model="nome" placeholder="Digite seu nome">
                </div>

                <div class="input-container">
                    <label for="pao">Escolha seu pão: </label>
                    <select name="pao" id="pao" v-model="pao">
                        <option  value="" disabled> 
                            Selecione seu Pão
                        </option>
                        <option  v-for="pao in paes" :key="pao.id" :value="pao.tipo">
                            {{ pao.tipo }}
                        </option>
                    </select>
                </div>
                
                <div class="input-container">
                    <label for="carne">Escolha sua carne: </label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="" disabled>
                            Selecione seu Carne
                        </option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
                            {{ carne.tipo }}
                        </option>
                    </select>
                </div>

                <div id="opcionais-container" class="input-container">
                    <label id="opcionais-title" for="opcionais">Selecione um Adicional Opcional:</label>
                    <div class="checkbox-container" v-for="opcao in opcionaisData" :key="opcao.id">
                        <input type="checkbox" name="opcionais" id="opcionais" v-model="opcionais" :value="opcao.tipo">
                        <span>{{ opcao.tipo }}</span>
                    </div>
                </div>

                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar meu Hamburguer">
                </div>

            </form>
        </div>
    </div>
</template>

<script>
 import Message from "../components/Message.vue"
    export default{
        name: 'BurgerForm',
        components: {
            Message,
        },
        
        data () {
            return{
                paes: null,
                carnes: null,
                opcionaisData: null,

                nome: null,
                pao:null,
                carne: null,
                opcionais: [],
                msg: null,
            }
        },
        
        methods: {
            async getIngredientes() {
                const req = await fetch("http://localhost:3000/ingredientes");
                const data = await req.json();

                this.paes = data.paes;
                this.carnes = data.carnes;
                this.opcionaisData = data.opcionais;
            },

            async creatBruger(e){

                e.preventDefault();
                
                const data = {
                    nome:       this.nome,
                    pao:        this.pao,
                    carne:      this.carne,
                    opcionais:  Array.from(this.opcionais),
                    satatus:    "Solicitado"
                }

                const dataJSON = JSON.stringify(data);

                const req = await fetch("http://localhost:3000/burgers", {
                    method: "POST",
                    headers: {"Content-Type": "application/json"},
                    body: dataJSON
                });

                this.msg =  `Pedido de ${this.nome} realizado com sucesso!!`;
                setTimeout(() => this.msg = "", 3000);
                const res =  await req.json();

                console.log(res);

                this.nome = "";
                this.pao = "";
                this.carne = "";
                this.opcionais = [];

            }
        },
        mounted() {
            this.getIngredientes();
        }
    }
</script>

<style scoped>
    #burger-form {
        max-width: 400px;
        margin: 0 auto;
    }
    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }
    label {
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #fcba03;
    }

    input, 
    select {
        padding: 5px 10px;
        width: 300px;
    }

    #opcionais-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }
    .checkbox-container span,
    .checkbox-container input {
        width: auto;
    }

    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
        background-color: #222;
        color: #fcba03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .submit-btn:hover {
        background-color: transparent;
        color: #222;
        border: 2px solid #fcba03;

    }

</style>