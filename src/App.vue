<template>
  <div id="app">
    <div class="futurist-background">
      <div class="app-container">
        <header class="app-header">
          <h1 class="title">Cadastro de Clientes</h1>
          <p class="subtitle">Sistema de gerenciamento futurista</p>
        </header>
        
        <main class="main-content">
          <form @submit.prevent="cadastrarCliente" class="futurist-form">
            <MeuComponenteFuturista
              id="nome"
              label="Nome completo"
              placeholder="Digite o nome completo"
              v-model="cliente.nome"
              required
              icon="👤"
            />
            
            <MeuComponenteFuturista
              id="email"
              label="E-mail"
              placeholder="seu@email.com"
              type="email"
              v-model="cliente.email"
              required
              icon="✉"
            />
            
            <MeuComponenteFuturista
              id="telefone"
              label="Telefone"
              placeholder="(00) 00000-0000"
              v-model="cliente.telefone"
              required
              icon="📱"
            />
            
            <MeuComponenteFuturista
              id="endereco"
              label="Endereço"
              placeholder="Rua, número, bairro, cidade"
              v-model="cliente.endereco"
              required
              icon="🏠"
            />
            
            <MeuComponenteFuturista
              id="cpf"
              label="CPF"
              placeholder="000.000.000-00"
              v-model="cliente.cpf"
              required
              icon="🔐"
            />
            
            <button type="submit" class="futurist-button">
              <span class="button-text">Cadastrar</span>
              <span class="button-icon">🚀</span>
            </button>
          </form>
          
          <div v-if="clientesCadastrados.length > 0" class="clientes-container">
            <h2 class="clientes-title">Clientes Cadastrados</h2>
            <div class="clientes-grid">
              <div v-for="(cliente, index) in clientesCadastrados" :key="index" class="cliente-card">
                <div class="card-header">
                  <h3>{{ cliente.nome }}</h3>
                  <span class="card-badge">#{{ index + 1 }}</span>
                </div>
                <div class="card-content">
                  <p><span class="info-label">Email:</span> {{ cliente.email }}</p>
                  <p><span class="info-label">Telefone:</span> {{ cliente.telefone }}</p>
                  <p><span class="info-label">CPF:</span> {{ cliente.cpf }}</p>
                </div>
                <div class="card-footer">
                  <span class="address-truncated">{{ cliente.endereco }}</span>
                </div>
              </div>
            </div>
          </div>
        </main>
      </div>
    </div>
  </div>
</template>

<script>
import MeuComponenteFuturista from './components/MeuComponente.vue'

export default {
  name: 'App',
  components: {
    MeuComponenteFuturista
  },
  data() {
    return {
      cliente: {
        nome: '',
        email: '',
        telefone: '',
        endereco: '',
        cpf: ''
      },
      clientesCadastrados: []
    }
  },
  methods: {
    cadastrarCliente() {
      if (this.validarFormulario()) {
        this.clientesCadastrados.push({...this.cliente});
        this.limparFormulario();
        
        // Efeito de notificação
        this.mostrarNotificacao('Cliente cadastrado com sucesso!', 'sucesso');
      }
    },
    validarFormulario() {
      // Validação básica - todos os campos são obrigatórios
      return Object.values(this.cliente).every(value => value.trim() !== '');
    },
    limparFormulario() {
      this.cliente = {
        nome: '',
        email: '',
        telefone: '',
        endereco: '',
        cpf: ''
      };
    },
    mostrarNotificacao(mensagem, tipo) {
      // Aqui você pode implementar um sistema de notificação
      alert(mensagem); // Substitua por um toast notification estilizado
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: linear-gradient(135deg, #000000, #000000, #000000);
  color: white;
  min-height: 100vh;
}

.futurist-background {
  min-height: 100vh;
  padding: 2rem;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  background: 
    radial-gradient(circle at 10% 20%, rgba(197, 11, 11, 0.2) 0%, transparent 20%),
    radial-gradient(circle at 90% 70%, rgba(0, 255, 208, 0.2) 0%, transparent 20%);
}

.app-container {
  width: 100%;
  max-width: 800px;
}

.app-header {
  text-align: center;
  margin-bottom: 3rem;
}

.title {
  font-size: 2.5rem;
  font-weight: 800;
  background: linear-gradient(90deg, #e6e6e6, #1c1e1d);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  margin-bottom: 0.5rem;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

.subtitle {
  color: rgba(230, 255, 7, 0.7);
  font-size: 1.1rem;
}

.futurist-form {
  background: rgba(20, 20, 30, 0.6);
  backdrop-filter: blur(12px);
  border-radius: 20px;
  padding: 2.5rem;
  margin-bottom: 3rem;
  box-shadow: 
    0 15px 35px rgba(0, 0, 0, 0.3),
    inset 2px 2px 5px rgba(255, 255, 255, 0.05),
    inset -2px -2px 5px rgba(0, 0, 0, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.futurist-button {
  width: 100%;
  padding: 1.2rem;
  background: linear-gradient(90deg, #6e45e2, #88d3ce);
  border: none;
  border-radius: 12px;
  color: white;
  font-weight: 600;
  font-size: 1.1rem;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 0.8rem;
  transition: all 0.3s ease;
  box-shadow: 0 5px 15px rgba(110, 69, 226, 0.4);
  margin-top: 1rem;
}

.futurist-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(110, 69, 226, 0.6);
}

.futurist-button:active {
  transform: translateY(0);
}

.clientes-container {
  background: rgba(20, 20, 30, 0.6);
  backdrop-filter: blur(12px);
  border-radius: 20px;
  padding: 2rem;
  box-shadow: 
    0 15px 35px rgba(0, 0, 0, 0.3),
    inset 2px 2px 5px rgba(255, 255, 255, 0.05),
    inset -2px -2px 5px rgba(0, 0, 0, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.clientes-title {
  font-size: 1.8rem;
  margin-bottom: 1.5rem;
  color: rgba(255, 255, 255, 0.9);
  text-align: center;
}

.clientes-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1.5rem;
}

.cliente-card {
  background: rgba(255, 255, 255, 0.7);
  border-radius: 15px;
  padding: 1.5rem;
  box-shadow: 0 5px 15px rgb(247, 247, 245);
  transition: transform 0.3s ease;
  border: 1px solid rgba(241, 240, 240, 0.05);
}

.cliente-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  padding-bottom: 0.8rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.card-header h3 {
  font-size: 1.2rem;
  color: #88d3ce;
}

.card-badge {
  background: linear-gradient(90deg, #6e45e2, #88d3ce);
  padding: 0.3rem 0.6rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: bold;
}

.card-content p {
  margin-bottom: 0.5rem;
  font-size: 0.9rem;
}

.info-label {
  color: rgba(255, 255, 255, 0.7);
  font-weight: 600;
}

.card-footer {
  margin-top: 1rem;
  padding-top: 0.8rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.address-truncated {
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.6);
  display: -webkit-box;
  -webkit-line-clamp: 2;
  line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* Animações */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

.app-container {
  animation: fadeIn 0.8s ease-out;
}

.cliente-card {
  animation: fadeIn 0.5s ease-out;
}

/* Responsividade */
@media (max-width: 768px) {
  .futurist-background {
    padding: 1rem;
  }
  
  .title {
    font-size: 2rem;
  }
  
  .futurist-form {
    padding: 1.5rem;
  }
  
  .clientes-grid {
    grid-template-columns: 1fr;
  }
}
</style>