# Comandos Práticos - Módulo 05: Automação, Cron e Systemd

Guia de execução passo a passo dos comandos apresentados nas aulas práticas do módulo. Compatível com o Ubuntu 24.04 LTS.

---

## Tópico 1: Automação de Tarefas com Shell Script

### Preparação do Cenário:
```bash
mkdir -p ~/cenario-script/projeto/{logs,cache} && touch ~/cenario-script/projeto/logs/{app1.log,app2.log} ~/cenario-script/projeto/cache/temp.data && clear && echo "=== Cenário M05-T01 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Acessando a Pasta de Trabalho
```bash
cd ~/cenario-script
```

#### 2. Escrevendo o Script de Limpeza com o Nano
```bash
nano limpar-projeto.sh
```
- Digite ou cole o conteúdo abaixo:
```bash
#!/usr/bin/env bash

echo "=== Iniciando Faxina do Projeto ==="
ALVO="projeto"

# Verificando se a pasta existe antes de executar
if [ -d "$ALVO" ]; then
    echo "Pasta $ALVO encontrada. Limpando logs e caches temporarios..."
    rm -f "$ALVO"/logs/*.log
    rm -f "$ALVO"/cache/*.data
    echo "Limpeza concluida com sucesso!"
else
    echo "Erro: A pasta $ALVO nao foi encontrada!"
fi
```
- Salve com `Ctrl + O`, tecle `Enter` e saia com `Ctrl + X`

#### 3. Concedendo Permissão de Execução (+x)
```bash
chmod +x limpar-projeto.sh
```

#### 4. Executando o Script e Conferindo os Resultados
```bash
./limpar-projeto.sh
```
```bash
ls projeto/logs
```

---

## Tópico 2: Agendamento de Tarefas com Cron

### Preparação do Cenário:
```bash
mkdir -p ~/cenario-cron && clear && echo "=== Cenário M05-T02 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Estrutura dos Campos do Cron
- `* * * * * comando` (Minuto | Hora | Dia do Mês | Mês | Dia da Semana)

#### 2. Editando a Tabela de Agendamentos do Usuário
```bash
crontab -e
```
- Adicione a linha abaixo no final do arquivo para rodar a cada minuto:
```bash
* * * * * date >> $HOME/cenario-cron/auditoria.log
```
- Salve com `Ctrl + O`, tecle `Enter` e feche com `Ctrl + X`

#### 3. Listando Agendamentos e Inspecionando a Execução
```bash
crontab -l
```
*(Aguarde cerca de 1 minuto para o primeiro registro)*
```bash
cat ~/cenario-cron/auditoria.log
```

---

## Tópico 3: Gerenciamento de Serviços com Systemd

### Preparação do Cenário:
```bash
printf '#!/bin/bash\nwhile true; do echo "API rodando em \$(date)"; sleep 5; done\n' > ~/worker-teste.sh && chmod +x ~/worker-teste.sh && clear && echo "=== Cenário M05-T03 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Criando o Arquivo de Serviço no Systemd
```bash
sudo nano /etc/systemd/system/meu-worker.service
```
- Cole a estrutura de configuração:
```ini
[Unit]
Description=Meu Servidor de Teste
After=network.target

[Service]
Type=simple
ExecStart=/bin/bash /home/ubuntu/worker-teste.sh
Restart=always

[Install]
WantedBy=multi-user.target
```
*(Nota: certifique-se de que o caminho do usuário corresponde à sua pasta de usuário no Ubuntu)*
- Salve com `Ctrl + O`, tecle `Enter` e feche com `Ctrl + X`

#### 2. Recarregando e Gerenciando o Serviço
```bash
sudo systemctl daemon-reload
```
```bash
sudo systemctl start meu-worker
```
```bash
sudo systemctl status meu-worker
```
```bash
sudo systemctl enable meu-worker
```

#### 3. Acompanhando os Logs do Serviço em Tempo Real
```bash
journalctl -u meu-worker -f
```
*(Pressione `Ctrl + C` para interromper o acompanhamento)*

---

### Limpeza dos Cenários (Opcional):
```bash
sudo systemctl stop meu-worker 2>/dev/null || true
sudo systemctl disable meu-worker 2>/dev/null || true
sudo rm -f /etc/systemd/system/meu-worker.service
sudo systemctl daemon-reload
crontab -r 2>/dev/null || true
rm -rf ~/cenario-script ~/cenario-cron ~/worker-teste.sh
```
