# Comandos Práticos - Módulo 01: Terminal e Sistema de Arquivos

Guia de execução passo a passo dos comandos apresentados nas aulas práticas do módulo. Compatível com o Ubuntu 24.04 LTS.

---

## Tópico 1: Primeiros Comandos e Produtividade

### Preparação do Ambiente:
```bash
clear && echo "=== Ambiente de Gravação M01-T01 Pronto ==="
```

### Sequência de Comandos:

#### 1. Identificando Usuário, Máquina e Sistema
```bash
whoami
```
```bash
hostname
```
```bash
uname -s
```
```bash
uname -a
```

#### 2. Executando Comandos com Opções (Flags)
```bash
date
```
```bash
date +"%Y-%m-%d"
```
```bash
date --iso-8601
```

#### 3. Atalhos de Produtividade no Terminal
- **Autocompletar:** Digite `whoa` e pressione `Tab`
- **Interromper comando:** Execute `sleep 20` e pressione `Ctrl + C`
- **Limpar a tela:** Pressione `Ctrl + L`

#### 4. Consultando o Histórico Recente
```bash
history 5
```

---

## Tópico 2: Navegação no Sistema de Arquivos

### Preparação do Cenário:
```bash
mkdir -p ~/cenario-web/projeto-legado/{public,src,logs} && touch ~/cenario-web/projeto-legado/src/index.js ~/cenario-web/projeto-legado/public/index.html ~/cenario-web/projeto-legado/.env.example && clear && echo "=== Cenário M01-T02 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Verificando a Localização Atual
```bash
pwd
```

#### 2. Listando Arquivos e Pastas com Detalhes e Ocultos
```bash
ls
```
```bash
ls -la
```
```bash
ls -lah
```

#### 3. Navegando entre Diretórios (Absoluto e Relativo)
```bash
cd ~/cenario-web/projeto-legado
```
```bash
pwd
```
```bash
ls -lah
```
```bash
cd ..
```
```bash
pwd
```
```bash
cd ~
```
```bash
cd -
```

---

## Tópico 3: Manipulação de Arquivos e Pastas

### Preparação do Cenário:
```bash
mkdir -p ~/cenario-projeto/templates && echo "PORT=3000" > ~/cenario-projeto/templates/env.example && touch ~/cenario-projeto/app.temp.js && clear && echo "=== Cenário M01-T03 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Acessando a Pasta de Trabalho
```bash
cd ~/cenario-projeto
```

#### 2. Criando a Estrutura de Pastas do Site em Cascata
```bash
mkdir -p meu-site/src meu-site/public/css
```

#### 3. Criando, Copiando e Movendo Arquivos
```bash
touch meu-site/README.md
```
```bash
cp templates/env.example meu-site/.env
```
```bash
ls -la meu-site
```
```bash
mv app.temp.js meu-site/src/server.js
```
```bash
ls -la meu-site/src
```

#### 4. Exclusão Consciente e Localização
```bash
rm meu-site/README.md
```
```bash
find meu-site -name "*.js"
```
```bash
find meu-site -type f
```

---

### Limpeza dos Cenários (Opcional):
```bash
rm -rf ~/cenario-web ~/cenario-projeto
```
