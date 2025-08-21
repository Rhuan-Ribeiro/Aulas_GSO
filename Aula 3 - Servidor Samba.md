# Aula 3 – Compartilhamento de Arquivos com Samba no Ubuntu Server (14/08/2025)

## Objetivo da Aula

Nesta aula, os alunos aprenderão como instalar e configurar o **Samba** em um servidor Ubuntu para permitir o compartilhamento de arquivos em uma rede local, acessível por computadores com Windows, Linux ou macOS. O objetivo é entender os conceitos de compartilhamento em rede e configurar pastas acessíveis com diferentes permissões de acordo com os setores da empresa.

---

## Glossário de Termos

Antes de iniciar a configuração do Samba, é importante entender alguns termos relacionados a redes e compartilhamento de arquivos.

- **Samba**  
  Software que permite compartilhar arquivos e impressoras entre sistemas Linux/Unix e computadores com Windows.

- **SMB/CIFS**  
  Protocolos usados pelo Samba para compartilhamento de arquivos e impressoras em redes locais.

- **Servidor de Arquivos**  
  Um servidor responsável por armazenar e disponibilizar arquivos em uma rede.

- **Permissões de Acesso**  
  Regras que definem quem pode ler, gravar ou executar arquivos e diretórios.

- **Compartilhamento Público**  
  Pasta acessível por qualquer usuário da rede, sem necessidade de autenticação.

- **Compartilhamento Privado**  
  Pasta protegida, que requer usuário e senha para acesso.

- **`smb.conf`**  
  Arquivo principal de configuração do Samba, localizado geralmente em `/etc/samba/smb.conf`.

- **`smbpasswd`**  
  Comando usado para definir senhas dos usuários do Samba.

- **Grupo de Trabalho (Workgroup)**  
  Nome do grupo de computadores que compartilham recursos em uma rede local, principalmente em ambientes Windows.

---

# Configuração de Compartilhamento de Arquivos com Samba no Ubuntu

Este guia mostra como configurar o Samba para compartilhamento de arquivos em uma rede local, com diretórios públicos e privados para diferentes grupos de usuários.

---

## 1. Instalando o Samba

Atualize o sistema e instale o Samba:

```bash
sudo apt update
sudo apt install samba -y
```

Verifique se o serviço está ativo:

```bash
sudo systemctl status smbd
```

---

## 2. Criando Usuários

Crie os usuários do sistema. Usaremos a mesma senha (`password`) para todos os usuários neste exemplo.

```bash
sudo adduser --disabled-login --no-create-home alice
sudo smbpasswd -a alice

sudo adduser --disabled-login --no-create-home rafael
sudo smbpasswd -a rafael

sudo adduser --disabled-login --no-create-home fernanda
sudo smbpasswd -a fernanda
```

---

## 3. Criando Grupos

Crie os grupos que representarão os setores da empresa:

```bash
sudo groupadd ti
sudo groupadd rh
sudo groupadd financeiro
```

---

## 4. Adicionando Usuários aos Grupos

Adicione os usuários aos seus respectivos grupos:

```bash
sudo usermod -aG ti alice
sudo usermod -aG rh rafael
sudo usermod -aG financeiro fernanda
```

---

## 5. Criando a Estrutura de Diretórios

Crie os diretórios públicos e privados, organizados por setor:

```bash
# Diretório público
sudo mkdir -p /srv/samba/publico

# Diretórios privados
sudo mkdir -p /srv/samba/privado/rh
sudo mkdir -p /srv/samba/privado/financeiro
```

Defina os donos e permissões:

```bash
# Permissões gerais
sudo chown -R root:ti /srv/samba
sudo chmod -R 775 /srv/samba

# RH
sudo chown root:rh /srv/samba/privado/rh
sudo chmod 770 /srv/samba/privado/rh

# Financeiro
sudo chown root:financeiro /srv/samba/privado/financeiro
sudo chmod 770 /srv/samba/privado/financeiro

# Público
sudo chown root:ti /srv/samba/publico
sudo chmod 777 /srv/samba/publico
```

---

## 6. Configurando o Samba

Edite o arquivo de configuração principal:

```bash
sudo nano /etc/samba/smb.conf
```

Adicione as seguintes seções ao final do arquivo:

```ini
[Publico]
   path = /srv/samba/publico
   browsable = yes
   read only = no
   guest ok = yes

[RH]
   path = /srv/samba/privado/rh
   browsable = yes
   read only = no
   valid users = @rh @ti

[Financeiro]
   path = /srv/samba/privado/financeiro
   browsable = yes
   read only = no
   valid users = @financeiro @ti
```

Salve o arquivo e reinicie o serviço:

```bash
sudo systemctl restart smbd
```

---

## 7. Acessando o Compartilhamento pela Rede

### No Windows

1. Pressione `Win + R` e digite:  
   `\\IP_DO_SERVIDOR`
2. Insira o nome de usuário e senha configurados com `smbpasswd`.
3. Os diretórios acessíveis aparecerão conforme as permissões do usuário.

### No Linux

Monte os compartilhamentos no sistema de arquivos:

```bash
sudo mount -t cifs //IP_DO_SERVIDOR/Publico /mnt/publico -o guest
sudo mount -t cifs //IP_DO_SERVIDOR/RH /mnt/rh -o user=rafael
sudo mount -t cifs //IP_DO_SERVIDOR/Financeiro /mnt/financeiro -o user=fernanda
```

> Substitua `IP_DO_SERVIDOR` pelo IP real do servidor Samba.

---

## 8. Comandos Úteis

```bash
testparm                      # Verifica se a configuração do Samba está correta
sudo smbstatus                # Mostra os usuários conectados
sudo systemctl restart smbd  # Reinicia o serviço do Samba
```

---

## 9. Desligando o Servidor com Segurança

```bash
sudo init 0
```

> Este comando desliga o servidor imediatamente.

---

## Referências

- Samba Project: https://wiki.samba.org/
- Ubuntu Server Docs: https://ubuntu.com/server/docs
- Guia do Samba no Ubuntu: https://help.ubuntu.com/community/Samba
