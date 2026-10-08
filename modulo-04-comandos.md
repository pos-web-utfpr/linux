# Comandos Práticos - Módulo 04: Redes, Testes HTTP e SSH

Guia de execução passo a passo dos comandos apresentados nas aulas práticas do módulo. Compatível com o Ubuntu 24.04 LTS.

---

## Tópico 1: Inspeção de Rede e Testes com Curl

### Preparação do Cenário:
```bash
python3 -m http.server 8080 > /dev/null 2>&1 & clear && echo "=== Cenário M04-T01 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Inspecionando Endereços IP da Máquina
```bash
ip a
```
*(Identifique o loopback `127.0.0.1` e a interface de rede local com o seu IP)*

#### 2. Verificando Portas Abertas com o Utilitário SS
```bash
ss -tuln
```
```bash
ss -tuln | grep 8080
```
*(Observe o estado LISTEN e a porta vinculada)*

#### 3. Testando a Resposta HTTP Diretamente no Terminal
```bash
curl -I http://localhost:8080
```
*(A resposta esperada é o cabeçalho HTTP com status 200 OK)*

---

## Tópico 2: Conexões Seguras com Chaves SSH

### Preparação do Ambiente:
```bash
clear && echo "=== Cenário M04-T02 Pronto ==="
```

### Sequência de Comandos:

#### 1. Gerando o Par de Chaves Criptográficas com o Algoritmo ed25519
```bash
ssh-keygen -t ed25519 -C "aluno@pos.com"
```
- Pressione `Enter` para aceitar o local padrão sugerido (`~/.ssh/id_ed25519`)
- Pressione `Enter` duas vezes para confirmar sem senha de passphrase

#### 2. Inspecionando os Arquivos da Pasta Oculta ~/.ssh
```bash
ls -la ~/.ssh/
```
- `id_ed25519`: **Chave Privada** (confidencial, nunca compartilhar)
- `id_ed25519.pub`: **Chave Pública** (o seu cadeado, seguro para compartilhar)

#### 3. Exibindo a Chave Pública para Cadastro em Serviços (ex: GitHub)
```bash
cat ~/.ssh/id_ed25519.pub
```

---

## Tópico 3: Variáveis de Ambiente e Aliases

### Preparação do Ambiente:
```bash
touch ~/.bashrc && clear && echo "=== Cenário M04-T03 Pronto ==="
```

### Sequência de Comandos:

#### 1. Diferença entre Variáveis Locais e Exportadas
```bash
PORT=3000
echo $PORT
```
```bash
export PORT=3000
export NODE_ENV=production
```

#### 2. Configurando Variáveis e Atalhos Permanentes no ~/.bashrc
```bash
nano ~/.bashrc
```
- Adicione as seguintes linhas no final do arquivo:
```bash
# Configuracoes personalizadas do dev
export API_URL="https://api.meusite.com"
alias ll='ls -lah'
```
- Salve com `Ctrl + O`, tecle `Enter` e feche com `Ctrl + X`

#### 3. Recarregando as Configurações sem Fechar o Terminal
```bash
source ~/.bashrc
```
```bash
ll
```
```bash
echo $API_URL
```

---

### Limpeza dos Cenários (Opcional):
```bash
pkill -f "http.server 8080" 2>/dev/null || true
```
