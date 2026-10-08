# Comandos Práticos - Módulo 02: Permissões, Logs e Editores

Guia de execução passo a passo dos comandos apresentados nas aulas práticas do módulo. Compatível com o Ubuntu 24.04 LTS.

---

## Tópico 1: Permissões de Arquivos e Sudo

### Preparação do Cenário:
```bash
mkdir -p ~/cenario-permissoes/uploads && touch ~/cenario-permissoes/uploads/foto.png && chmod 000 ~/cenario-permissoes/uploads/foto.png && clear && echo "=== Cenário M02-T01 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Acessando a Pasta de Trabalho
```bash
cd ~/cenario-permissoes
```

#### 2. Diagnosticando a Falha de Permissão
```bash
cat uploads/foto.png
```
```bash
ls -l uploads/foto.png
```

#### 3. Corrigindo as Permissões com Chmod (644 para Arquivos e 755 para Pastas)
```bash
chmod 644 uploads/foto.png
```
```bash
chmod 755 uploads
```
```bash
ls -l uploads/foto.png
```
```bash
cat uploads/foto.png
```

---

## Tópico 2: Filtros e Análise de Logs com Grep

### Preparação do Cenário:
```bash
mkdir -p ~/cenario-logs && printf "2026-09-10 10:00:01 GET /home 200\n2026-09-10 10:00:05 POST /login 500\n2026-09-10 10:00:12 GET /produtos 200\n2026-09-10 10:01:30 GET /api/v1/checkout 500\n2026-09-10 10:02:00 GET /sobre 200\n" > ~/cenario-logs/access.log && clear && echo "=== Cenário M02-T02 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Acessando a Pasta de Trabalho
```bash
cd ~/cenario-logs
```

#### 2. Visualizando o Conteúdo Bruto do Log
```bash
cat access.log
```

#### 3. Filtrando Linhas de Erro com Grep
```bash
grep "500" access.log
```
```bash
cat access.log | grep "500"
```
```bash
grep -i "post" access.log
```

#### 4. Contando Linhas e Redirecionando a Saída
```bash
cat access.log | grep "500" | wc -l
```
```bash
grep "500" access.log > relatorio-erros.txt
```
```bash
cat relatorio-erros.txt
```
```bash
echo "=== Fim da Auditoria ===" >> relatorio-erros.txt
```
```bash
cat relatorio-erros.txt
```

---

## Tópico 3: Edição de Arquivos com Nano e Vim

### Preparação do Cenário:
```bash
mkdir -p ~/cenario-config && printf "DATABASE_URL=postgres://localhost:5432/antigo\nDEBUG=true\nPORT=3000\n" > ~/cenario-config/.env && clear && echo "=== Cenário M02-T03 Criado com Sucesso ==="
```

### Sequência de Comandos:

#### 1. Acessando a Pasta de Trabalho
```bash
cd ~/cenario-config
```

#### 2. Editando com o Nano
```bash
nano .env
```
- Altere `PORT=3000` para `PORT=8080`
- Pressione `Ctrl + O` e tecle `Enter` para salvar
- Pressione `Ctrl + X` para sair
```bash
cat .env
```

#### 3. Editando com o Vim
```bash
vim .env
```
- Pressione a tecla `i` para entrar em modo de inserção (aparece `-- INSERT --` no rodapé)
- Altere `DEBUG=true` para `DEBUG=false`
- Pressione a tecla `Esc` para sair do modo de inserção
- Digite `:wq` e tecle `Enter` para salvar e sair
*(Nota: para sair sem salvar alterações no Vim, pressione `Esc`, digite `:q!` e tecle `Enter`)*
```bash
cat .env
```

---

### Limpeza dos Cenários (Opcional):
```bash
rm -rf ~/cenario-permissoes ~/cenario-logs ~/cenario-config
```
