---
title: "Erro no Boot do Linux: File System Check (fsck) Requerido"
date: 2025-02-11T11:30:03+00:00
author: "Alessandro César Rosão"
draft: true
categories: [Linux, Solução de Problemas, Terminal]
tags: [boot, fsck, linux, sistema de arquivos, erro de boot]
---

## Introdução
Se ao iniciar o seu sistema Linux você se deparou com a seguinte mensagem de erro:

```bash
/dev/xvda3: UNEXPECTED INCONSISTENCY; RUN fsck MANUALLY.
(i.e., without -a or -p options)
fsck exited with status code 4
Failure: File system check of the root filesystem failed
The root filesystem on /dev/xvda3 requires a manual fsck
```

Isso indica que o sistema de arquivos está corrompido e precisa ser verificado manualmente. Vamos entender o motivo e como corrigir isso!

---

## Por que esse erro acontece?
Esse problema geralmente ocorre devido a:

- **Desligamento inesperado** (queda de energia, travamento do sistema);
- **Setores defeituosos no disco**;
- **Erros no journal do sistema de arquivos**;
- **Problemas na inicialização do disco ou corrupção de inodes**.

O Linux detecta inconsistências no sistema de arquivos e impede o boot para evitar danos maiores.

---

## Como corrigir o erro?

### 1 Passo: Acessar o modo de recuperação
Quando você se deparar com a tela `initramfs`, você já está no modo de recuperação.

Digite o comando abaixo para verificar e corrigir os erros automaticamente:

```bash
fsck -y /dev/xvda3
```

Explicação:
- `fsck` → Comando para verificar e corrigir erros no sistema de arquivos.
- `-y` → Responde "sim" automaticamente para todas as correções necessárias.
- `/dev/xvda3` → Substitua pelo seu dispositivo, caso seja diferente.

Se o comando acima não resolver, tente forçar a verificação com:

```bash
fsck -f /dev/xvda3
```

---

### 2 Passo: Reiniciar o sistema
Depois que o `fsck` concluir as correções, reinicie o sistema:

```bash
reboot
```

Se tudo correu bem, seu sistema deve iniciar normalmente! 🎉

---

## Caso o erro persista
Se, após rodar o `fsck`, o problema continuar, pode haver falhas físicas no disco. Para verificar erros de hardware, rode:

```bash
dmesg | grep -i error
```

Se aparecerem erros relacionados ao disco, considere substituí-lo.

---

## Conclusão
O erro "UNEXPECTED INCONSISTENCY" ocorre quando há corrupção no sistema de arquivos. Na maioria dos casos, executar `fsck -y /dev/xvda3` resolve o problema rapidamente. No entanto, se o erro persistir, pode ser necessário até mesmo substituir o disco.
