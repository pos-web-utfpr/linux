# Comandos Práticos - Módulo 06: Segurança e Harness de IA

Guia de execução passo a passo dos comandos apresentados nas aulas práticas do módulo. Compatível com o Ubuntu 24.04 LTS.

---

## Tópico 1: Fundamentos de Harness de IA no Linux

### Preparação do Ambiente:
```bash
clear && echo "=== Cenário M06-T01 Pronto ==="
```

### Sequência de Comandos:

#### 1. Validando Códigos de Saída ($?) no Linux
- **Execução com sucesso (retorna 0):**
```bash
ls /home
```
```bash
echo "Codigo de saida: $?"
```

- **Execução com erro (retorna diferente de 0):**
```bash
ls /pasta-que-nao-existe-12345 2>/dev/null
```
```bash
echo "Codigo de saida: $?"
```

#### 2. Controle de Contenção e Limite de Tempo com Timeout
```bash
timeout 3s sleep 10
```
```bash
echo "Codigo de saida do timeout: $?"
```
*(O código `124` comprova a interrupção automática do processo pelo limite de tempo estrito)*

---

## Tópico 2: Segurança de Rede e Firewall com UFW

### Preparação do Ambiente:
```bash
sudo ufw status && clear && echo "=== Cenário M06-T02 Pronto ==="
```

### Sequência de Comandos:

#### 1. Liberando a Porta do SSH (Passo Fundamental antes de Ativar o Firewall)
```bash
sudo ufw allow 22/tcp
```

#### 2. Liberando as Portas Padrão de Servidores Web (HTTP e HTTPS)
```bash
sudo ufw allow 80/tcp
```
```bash
sudo ufw allow 443/tcp
```

#### 3. Ativando o Firewall e Inspecionando o Relatório de Regras
```bash
sudo ufw enable
```
*(Ao ser questionado se deseja prosseguir, confirme digitando `y` e teclando Enter)*
```bash
sudo ufw status verbose
```

---

## Tópico 3: Ferramentas CLI e Agentes de IA

### Preparação do Cenário:
```bash
mkdir -p ~/cenario-cli && echo "console.log('teste de depuracao')" > ~/cenario-cli/server.js && clear && echo "=== Cenário M06-T03 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Acessando a Pasta de Trabalho
```bash
cd ~/cenario-cli
```

#### 2. Visualização de Arquivos no Terminal
- Visualização tradicional com o cat:
```bash
cat server.js
```
- Visualização profissional com numeração de linhas:
```bash
cat -n server.js
```

#### 3. Consulta Orientada com Assistentes de IA
- Exemplo de prompt estruturado para o terminal:
  > *"Explique detalhadamente o que cada flag deste comando realiza antes de executá-lo no terminal: `sudo ufw allow 80/tcp`."*

---

### Limpeza dos Cenários (Opcional):
```bash
sudo ufw disable 2>/dev/null || true
rm -rf ~/cenario-cli
```
