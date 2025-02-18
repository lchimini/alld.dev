---
title: "Guia Completo do rclone: Domine a Sincronização de Nuvens com Comandos Avançados!"
date: 2025-02-18T11:36:03+00:00
author: "Alessandro César Rosão"
categories: ["Linux", "Terminal", "Rclone"]
tags: ["rclone", "terminal", "linux", "sincronizacao"]
---

# 🚀 Introdução ao rclone

O **rclone** é um poderoso "canivete suíço" para gerenciamento de armazenamentos em nuvem. Neste guia, você aprenderá desde comandos básicos até técnicas profissionais de otimização!

---

## 📥 Instalação Básica

```bash
# Linux (Debian/Ubuntu)
curl https://rclone.org/install.sh | sudo bash

# macOS
brew install rclone

# Windows
choco install rclone
```

---

## 🔧 Comandos Essenciais

### 📂 Listar arquivos
```bash
rclone ls remote:nome_do_bucket
```

### 📤 Copiar arquivos
```bash
rclone copy origem destino:/pasta
```

### 🔄 Sincronizar diretórios
```bash
rclone sync origem destino:/pasta --progress
```

### 🗑️ Excluir arquivos
```bash
rclone delete remote:pasta_obsoleta
```

---

## ⚡ Comandos Avançados (Turbo Mode!)

### 📊 Verificar espaço utilizado
```bash
rclone about remote:
```

### 🕵️ Listar diretórios
```bash
rclone lsd remote:
```

### 📏 Calcular tamanho
```bash
rclone size remote:pasta_importante
```

### 🧹 Limpar lixeira
```bash
rclone cleanup remote:
```

---

## 🛠️ Flags de Alta Performance
Parâmetros profissionais para otimizar suas transferências:

| Flag | Descrição | Valor Recomendado |
|------|-----------|-------------------|
| `-P` | Progresso detalhado | Sempre usar |
| `--transfers` | Transferências paralelas | 2-4 |
| `--checkers` | Verificadores simultâneos | 2-4 |
| `--tpslimit` | Limite de transações/segundo | 4 |
| `--onedrive-chunk-size` | Tamanho do chunk (OneDrive) | 10M |
| `--bwlimit` | Limite de banda | 15M |
| `--low-level-retries` | Tentativas de recuperação | 10 |
| `--retries` | Tentativas normais | 5 |
| `--timeout` | Tempo máximo por operação | 10m |
| `--ignore-checksum` | Ignora verificação de hash | Use com cuidado! |
| `--ignore-case-sync` | Ignora diferença de caixa | Para sistemas case-insensitive |
| `--log-file` | Arquivo de log personalizado | `/caminho/do/log.log` |
| `--log-format` | Formato do log | `date,time` |
| `--user-agent` | Identificação personalizada | `"ISV|rclone.org|rclone/v1.50.2"` |

---

## 💡 Exemplo de Uso Profissional

### Sincronização Otimizada para OneDrive
```bash
rclone sync -P --transfers 2 --checkers 2 --tpslimit 4 \
--onedrive-chunk-size 10M --bwlimit 15M \
--low-level-retries 10 --retries 5 --timeout 10m \
--ignore-checksum --ignore-case-sync \
--log-file /home/ubuntu/logs-rclone/rclone-sync1.log \
--log-format "date,time" --log-level INFO \
--ignore-size \
--user-agent "ISV|rclone.org|rclone/v1.50.2" \
/local/path/ oneDrive:remote_folder
```

### ⏰ Agendamento com Cron (Backup Diário)
```bash
0 2 * * * /usr/bin/rclone sync -P /dados importantes:backup --bwlimit "08:00,15M 23:00,off"
```

---

## ⚠️ Dicas de Segurança

1. **Teste antes de sincronizar!** Use `--dry-run`
2. **Cuidado com `--ignore-checksum`** - Desativa verificação de integridade
3. **Monitore logs** regularmente: `tail -f /home/ubuntu/logs-rclone/rclone-sync1.log`

---

## 🔗 Recursos Adicionais

- [📚 Documentação Oficial](https://rclone.org/)
- [💬 Fórum de Suporte](https://forum.rclone.org/)
- [🐙 GitHub do Projeto](https://github.com/rclone/rclone)
