# Acesso Remoto com SSH (Secure Shell)

SSH é um protocolo que permite conectar-se de forma segura a outro computador via linha de comando. É fundamental para administrar servidores remotamente.

---

### Instalando o OpenSSH Server no Ubuntu

- Instale o OpenSSH Server durante a instalação do Ubuntu Server, marcando a opção no instalador.

- Caso tenha esquecido, ou precise instalar depois, utilize os comandos abaixo:

```bash
sudo apt update
sudo apt install openssh-server -y
```

### Verificando se o serviço SSH está ativo

Para garantir que o serviço SSH está rodando corretamente, execute:

```bash
sudo systemctl status ssh
```

O status deverá indicar **"active (running)"** para confirmar que o servidor SSH está funcionando.

### Descobrindo o IP do Servidor

Para conectar-se ao servidor, é necessário conhecer o endereço IP da máquina. Use o comando:

```bash
ip a
```

Procure pelo endereço IP da interface de rede ativa (geralmente algo como eth0, ens33 ou enp0s3).

### Descobrindo qual usuário está logado

Para saber qual usuário está atualmente conectado no servidor (ou para usar na conexão SSH), utilize:

```bash
whoami
```

Esse comando retorna o nome do usuário em uso no terminal atual.

Obs.: No Windows, podemos usar o mesmo comando no PowerShell, mas também há uma forma alternativa de fazê-lo: digite no PowerShell **$env:USERNAME**.

### Conectando-se ao servidor via SSH

No terminal do seu computador local (Linux e/ou Windows), utilize o comando abaixo para se conectar ao servidor:

```bash
ssh usuario@IP_DO_SERVIDOR
```

- Substitua **usuario** pelo nome do seu usuário no servidor.
- Substitua **IP_DO_SERVIDOR** pelo IP obtido no comando anterior.

#### Exemplo:

```bash
ssh joao@192.168.1.100
```

# Encerrando a sessão SSH

Para finalizar a conexão SSH, digite:

```bash
exit
```

Isso encerrará a sessão e fechará a conexão com o servidor.