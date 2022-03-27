<template>
    <div>
        <Message :msg="msg" v-show="msg" />

        <div>
            <form id="burger-form" @submit="createBurger">

            <div class="input-container">
                <label for="nome">Nome do cliente</label>
                <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
            </div>

            <div class="input-container">
                <label for="pao">Escolha o pao:</label>
                <select name="pao" id="pao" v-model="pao">
                    <option value="">Selecione o seu pao</option>
                    <!-- Puxando com o v-for os ingredientes do banco e listando no template -->
                    <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                </select>
            </div>

            <div class="input-container">
                <label for="carne">Selecione a carne do seu Burger:</label>
                <select name="carne" id="carne" v-model="carne">
                    <option value="">Escolha a carne do seu Burger</option>
                    <!-- Puxando com o v-for os ingredientes do banco e listando no template -->
                    <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                </select>
            </div>

            <div id="opcionais-container" class="input-container">
                <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
                <!-- Puxando com o v-for os ingredientes do banco e listando no template -->
                <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                    <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                    <span>{{ opcional.tipo }}</span>
                </div>
                
            </div>

             <div class="input-container">
                <input type="submit" class="submit-btn" value="Criar meu Burger!">
             </div>

            </form>
        </div>

    </div>
</template>

<script>
import Message from './Message.vue'

export default {
    // name componet
    name: "BurgerForm",

    components: {
        Message,
    },
    //data 
    data(){
        return {
            // dados que vem serve
            paes: null,
            carnes: null,
            opcionaisdata: null,
            //dados que sao enviados
            nome: null,
            pao:null,
            carne: null,
            opcionais:[],
            msg: null
            
        }
    },
    // methods
    methods : {
        async getIngredientes(){
            // Criando request
            const req = await fetch("http://localhost:3000/ingredientes"); 
            const data = await req.json();

            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
        },
        // method post (enviar form)
        async createBurger(e) {
            
            e.preventDefault();

            const data = {
                nome: this.nome,
                pao: this.pao,
                carne: this.carne,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            }
        // Chamando o array para texto    
            const dataJson = JSON.stringify(data);
        // Enviando para o backend method post (enviar form)
            const req = await fetch("http://localhost:3000/burgers",{
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            });

            const res = await req.json();

            // Message do sistema
            this.msg = `Pedido numero : ${res.id} realizado com sucesso`;

            // Limpando message do sistema 
            setTimeout(() => this.msg = '',  3000);


            // Limpar os campos

            this.nome = "";
            this.carne = "";
            this.pao = "";
            this.opcionais = "";

        }
    },
    mounted() {
        this.getIngredientes()
    }
}
</script>

<style scoped>
    #burger-form{
        max-width: 400px;
        margin: auto;
    }

    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label {
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #FCBA03;
    }

    input, select {
        padding:  5px 10px;
        widows: 300px;
    }

    #opcionais-container {
        flex-direction: row;
    }

    #opcionais-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: flex-start;
    
    }

    .checkbox-container span,
    .checkbox-container input{
        width: auto;
    }

    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
        background-color: #222;
        color: #FCBA03;
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
    }

</style>