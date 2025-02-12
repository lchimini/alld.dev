---
title: "Como Redefinir a Senha de Root no Linux via GRUB"
date: 2025-02-12T11:36:03+00:00
author: "Alessandro César Rosão"
categories: ["Linux", "Terminal", "GRUB"]
tags: ["grub", "terminal", "reset password", "linux", "resetar senha linux"]
---

Esquecer a senha de root no Linux pode ser um problema, mas felizmente há uma solução rápida e eficaz utilizando o GRUB (Grand Unified Bootloader). Este guia vai te ajudar a redefinir a senha de root em poucos passos. Vamos lá!

## 🚀 Quando Usar Este Método?
Este procedimento é ideal para situações em que:
- Você esqueceu a senha de root.
- Precisa acessar o sistema para realizar manutenções urgentes.
- Não há outro usuário com permissões administrativas disponível.

**⚠️ Atenção:** Este método requer acesso físico à máquina e permissão para modificar o processo de inicialização. Use-o com responsabilidade, pois ele pode comprometer a segurança do sistema se utilizado de forma inadequada.

---

## 📝 Passo a Passo

### 1. 🖥️ Acesse o GRUB
- Durante a inicialização do sistema, pressione e segure a tecla <kbd>Shift</kbd> (em sistemas BIOS) ou <kbd>Esc</kbd> (em sistemas UEFI) para acessar o menu do GRUB.
- Se o sistema iniciar muito rápido e você não conseguir acessar o GRUB, reinicie o computador e tente novamente.

### 2. ⚙️ Edite as Opções Avançadas
- No menu do GRUB, selecione a opção **"Opções Avançadas"**.
- Pressione a tecla <kbd>e</kbd> para editar os comandos de inicialização.

### 3. 🔍 Localize a Linha de Comando
- Navegue até a linha que começa com `linux /boot/vmlinuz`. Essa linha contém os parâmetros de inicialização do kernel.

### 4. ✏️ Modifique a Linha de Comando
- Apague o trecho final da linha, que contém `ro initrd=/install/initrd.gz quiet splash`. Esses parâmetros indicam que o sistema deve iniciar em modo somente leitura (`ro`) e ocultar mensagens de inicialização (`quiet splash`).
- Substitua por:  
  ```bash
  rw init=/bin/bash
  ```  
  - `rw`: Inicia o sistema em modo de leitura e escrita.
  - `init=/bin/bash`: Inicializa o sistema diretamente em um terminal Bash, ignorando o processo de login.

### 5. 💾 Salve e Reinicie
- Pressione <kbd>F10</kbd> para salvar as alterações e reinicializar o sistema. O sistema será iniciado em modo de recuperação, sem solicitar senha.

### 6. 🔄 Redefina a Senha de Root
- No terminal, execute o comando abaixo para alterar a senha de root:  
  ```bash
  passwd root
  ```  
  - Insira a nova senha duas vezes quando solicitado.
- Após redefinir a senha, reinicie o sistema com o comando:  
  ```bash
  reboot
  ```  
  Ou, se preferir, utilize:  
  ```bash
  exec /sbin/init
  ```  
  Isso reiniciará o sistema normalmente.

---

## 💡 Dicas Importantes
- **📂 Backup de Dados:** Sempre que for realizar alterações críticas no sistema, como redefinir senhas, é recomendável ter um backup dos seus dados importantes.
- **🔒 Segurança:** Após redefinir a senha, certifique-se de que o GRUB esteja protegido com uma senha para evitar que outras pessoas realizem alterações sem autorização.
- **🐧 Distribuições Diferentes:** O procedimento pode variar levemente dependendo da distribuição Linux utilizada. No entanto, o conceito básico é o mesmo.

---

## 🎉 Conclusão
Redefinir a senha de root no Linux é um processo simples quando você sabe como acessar e modificar o GRUB. Este método é uma ferramenta poderosa para administradores de sistema, mas deve ser usado com cuidado para evitar problemas de segurança.
