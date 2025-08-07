# Aula 2 – Instalando o Ubuntu Server em uma Máquina Virtual (07/08/2025)

## Objetivo da Aula

Nesta aula, o objetivo é guiar os alunos passo a passo na criação de uma máquina virtual com o Ubuntu Server utilizando o VirtualBox. A instalação será sem interface gráfica, reforçando o uso de linha de comando.

---

## Glossário de Termos

Antes de começarmos a instalação do Ubuntu Server, é importante entender alguns termos técnicos que surgem durante o processo. Esses conceitos ajudarão a tomar decisões informadas e compreender melhor o funcionamento de um servidor.

- **ISO**  
  Um arquivo que contém uma imagem completa de um disco (CD, DVD ou USB). A ISO do Ubuntu Server é usada como “instalador virtual” no VirtualBox.

- **Máquina Virtual (VM)**  
  Um ambiente que simula um computador real dentro de outro sistema operacional. Permite testar e instalar sistemas operacionais sem afetar seu sistema principal.

- **VirtualBox**  
  Software de virtualização que permite criar e gerenciar máquinas virtuais no seu computador.

- **Hostname**  
  Nome do computador na rede. Serve para identificar a máquina dentro da rede local ou pela internet.

- **Endereço IP**  
  Identificador numérico único de um dispositivo em uma rede.

- **IP Dinâmico (via DHCP)**  
  IP atribuído automaticamente pelo roteador. Pode mudar a cada reinicialização.

- **IP Estático (IP fixo)**  
  IP configurado manualmente, que permanece sempre o mesmo. Ideal para servidores, facilita o acesso remoto.

- **DHCP (Dynamic Host Configuration Protocol)**  
  Protocolo que distribui IPs automaticamente para dispositivos em uma rede.

- **Modo Bridge (no VirtualBox)**  
  Configuração de rede em que a máquina virtual se comporta como se estivesse diretamente conectada à rede física (como outro dispositivo real).

- **Proxy**  
  Servidor intermediário entre o computador e a internet. Frequentemente usado em redes corporativas. Pode ser deixado em branco na instalação doméstica.

- **Usuário sudo**  
  Conta de usuário com permissões administrativas. Pode usar o comando `sudo` para executar tarefas como administrador (root).

- **OpenSSH Server**  
  Serviço que permite conexões remotas seguras via terminal. Deve ser instalado durante a instalação do Ubuntu Server.

- **SSH (Secure Shell)**  
  Protocolo de rede que permite acessar e administrar servidores remotamente de forma segura, por meio da linha de comando.

- **Particionamento de Disco**  
  Processo de dividir o disco rígido em partes lógicas (partições) para organização do sistema e dos dados.

- **LVM (Logical Volume Manager)**  
  Sistema avançado de gerenciamento de volumes lógicos. Permite redimensionar partições com facilidade.

- **Snap**  
  Sistema de empacotamento e distribuição de software no Ubuntu. São pacotes autocontidos que agrupam um aplicativo e todas as suas dependências em um único arquivo, permitindo que funcionem em diversas distribuições Linux

---

## 1. O que é uma Máquina Virtual?

**Máquina Virtual (VM):** É uma simulação de um sistema computacional, onde um software emula o hardware e permite rodar sistemas operacionais de forma isolada.

### Vantagens:

- Testar sem afetar o sistema real.
- Rodar múltiplos SOs simultaneamente.
- Fácil backup e restauração (snapshots).
- Útil para treinar administração de servidores.

---

## 2. Requisitos

Antes de iniciar, verifique se você tem:

- VirtualBox instalado: [https://www.virtualbox.org](https://www.virtualbox.org)
- ISO do Ubuntu Server: [https://ubuntu.com/download/server](https://ubuntu.com/download/server)

> Recomendado: Baixar a última versão do Ubuntu Server LTS(Long Term Support), no caso é o Ubuntu Server 24.04 LTS

---

## 3. Criando a Máquina Virtual

1. **Abra o VirtualBox**
2. Clique em **"Novo"** e configure:
   - **Nome:** Ubuntu Server
   - **Tipo:** Linux
   - **Versão:** Ubuntu (64-bit)
3. Alocar recursos:
   - **Memória RAM:** mínimo 1024 MB (recomendado 4096 MB)
   - **Processadores:** mínimo 2
   - **EFI:** não habilite
4. Criar disco rígido virtual:
   - **Tipo:** VDI
   - **Armazenamento:** Dinamicamente alocado
   - **Tamanho:** mínimo 5 GB (recomendado 25 a 50 GB)

---

## 4. Configurações Recomendadas da Máquina Virtual

Antes de iniciar a instalação, é recomendável ajustar algumas configurações da VM para evitar problemas e melhorar o desempenho.

### Sistema

1. Acesse **Configurações > Sistema > Placa-Mãe**
   - Desmarque a opção **"Habilitar Relógio da Máquina em Hora UTC"** para evitar conflitos de horário.
2. Em **Configurações > Sistema > Processador**:
   - Marque **"Habilitar PAE/NX"**, necessário para sistemas operacionais modernos.
   - Se estiver no Windows, marque também **"Habilitar VT-x/AMD-V Aninhado"**  para melhor performance.

### Monitor

- Em **Configurações > Tela**, aumente a **memória de vídeo para 128 MB**. Isso garante melhor compatibilidade, mesmo em modo texto.

### Áudio

- Em **Configurações > Áudio**, desmarque a opção **"Habilitar Áudio"**, pois o servidor não utilizará som.

### Rede (Fundamental)

1. Vá em **Configurações > Rede**
2. Certifique-se de que a opção **"Habilitar Placa de Rede"** está ativada.
3. Em **Conectado a**, selecione: **"Placa de Rede em modo Bridge"**. Isso fará com que o servidor esteja acessível como um dispositivo da rede local.
4. Se possível, conecte-se via **cabo de rede** para garantir maior estabilidade e IP fixo via DHCP do roteador.

---

## 6. Instalação da ISO

1. Selecione a VM criada > clique em **"Configurações"**
2. Vá até **Armazenamento**
3. Clique em **"Vazio"** no controlador IDE
4. No ícone de disco (à direita), clique em **"Escolher arquivo de disco"**
5. Selecione o arquivo `.iso` do Ubuntu Server

1. Inicie a VM
2. Selecione a ISO do Ubuntu Server.
3. Clique em "Montar e Tentar Novo Boot".

## 7. Instalando o Ubuntu Server
1. Com a opção **"Try or Install Ubuntu Server"** selecionada, pressione **Enter**
2. Siga os passos do instalador:
   - Idioma: Inglês. Por ser o idioma original evita erros, se quiser pode mudar para Português do Brasil posteriormente.
   - Teclado: ABNT2 (se aplicável).
   - Base para Instalação: Ubuntu Server.
   - Rede: Automática via DHCP, depois mudaremos para IP fixo.
   - Configurações de Proxy: Pode pular por enquanto.
   - Aguarde a instalações dos pacotes.
   - Configuração de Armazenamento: Deixe a padrão. Não utilizaremos o gerenciamento de Volumes Lógicos da Distruibuição.
   - Parcionamento: Vamos usar o disco inteiro, vá em **"ubuntu-lv"** e edite o espaço para o máximo possível.
   - Preencha o seu nome.
   - Nome da máquina: `ubuntu-server`
   - Nome de usuário e senha. Esse vai ser o usuário do grupo sudo, que tem direito total no servidor.
   - Ubuntu Pro: Pule essa etapa, podemos configurar depois.
   - Configuração SSH: Pressione espaço para instalar OpenSSH server. Depois iremos configura-lo.
   - Snaps: Iremos instalar manualmente depois, pode pular.
   - Aguarde a Instalação e quando terminar vá para a opção **"Reboot Now"**

---

## 7. Primeira Inicialização

Após o término da instalação:

- Remova o disco ISO da VM (Configurações > Armazenamento > Remover disco óptico)
- Reinicie a VM

Você verá a tela de login em modo texto (CLI):

```
ubuntu-server login:
```

## 8. Desligando o Servidor

Para desligar o servidor basta usar o comando init

```
sudo init 0
```

---

## 9. Primeiros Comandos no Ubuntu Server

Após o login com seu usuário e senha, execute:

```bash
hostname        # Mostra o nome do host
ip a            # Exibe os endereços IP da máquina
uptime          # Exibe o tempo de atividade do sistema
sudo apt update # Atualiza a lista de pacotes
```
---

## Referências

- Ubuntu Server: https://ubuntu.com/server/docs
- VirtualBox Manual: https://www.virtualbox.org/manual/UserManual.html
