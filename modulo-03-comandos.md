# Comandos Práticos - Módulo 03: Processos, Recursos e Pacotes

Guia de execução passo a passo dos comandos apresentados nas aulas práticas do módulo. Compatível com o Ubuntu 24.04 LTS.

---

## Tópico 1: Identificação e Controle de Processos

### Preparação do Cenário:
```bash
python3 -c 'import time; [time.sleep(1) for _ in range(1000)]' & clear && echo "=== Cenário M03-T01 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Executando Tarefas em Segundo Plano com o Operador &
```bash
python3 -c 'import time; [time.sleep(1) for _ in range(100)]' &
```

#### 2. Localizando o Processo e o Número do PID
```bash
ps aux
```
```bash
ps aux | grep python
```
*(O número do PID está localizado na 2ª coluna da saída)*

#### 3. Finalizando Processos Travados
- Encerramento padrão e gracioso (SIGTERM):
```bash
kill <NUMERO_DO_PID>
```
- Encerramento forçado caso o processo não responda (SIGKILL):
```bash
kill -9 <NUMERO_DO_PID>
```
- Verificando a finalização:
```bash
ps aux | grep python
```

---

## Tópico 2: Monitoramento de CPU, Memória e Disco

### Preparação do Ambiente:
```bash
clear && echo "=== Cenário M03-T02 Pronto ==="
```

### Sequência de Comandos:

#### 1. Monitoramento Visual em Tempo Real com Htop
```bash
htop
```
- Pressione `F6` para ordenar a lista de processos por `%CPU` ou `%MEM`
- Pressione `q` para sair do htop

#### 2. Analisando a Memória RAM Realmente Disponível
```bash
free -h
```
*(Consulte a coluna **available**, que representa a memória disponível para novas aplicações)*

#### 3. Inspecionando Espaço em Disco
```bash
df -h
```
*(Observe o percentual de uso da partição raiz `/` na coluna Use%)*
```bash
du -sh *
```
*(Exibe o espaço ocupado por cada pasta no diretório atual)*

---

## Tópico 3: Gerenciamento de Pacotes com APT

### Preparação do Cenário:
```bash
mkdir -p ~/cenario-pacotes && echo "mock de release compilado versao 1.0" > ~/cenario-pacotes/versao.txt && tar -czf ~/cenario-pacotes/release-v1.tar.gz -C ~/cenario-pacotes versao.txt && rm ~/cenario-pacotes/versao.txt && clear && echo "=== Cenário M03-T03 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Acessando a Pasta de Trabalho
```bash
cd ~/cenario-pacotes
```

#### 2. Atualizando Repositórios e Instalando Pacotes com APT
```bash
sudo apt update
```
```bash
sudo apt install -y htop curl tree unzip
```

#### 3. Descompactando Arquivos de Release (.tar.gz)
```bash
ls -la
```
```bash
tar -xvf release-v1.tar.gz
```
```bash
cat versao.txt
```

---

### Limpeza dos Cenários (Opcional):
```bash
pkill -f "time.sleep" 2>/dev/null || true
rm -rf ~/cenario-pacotes
```
