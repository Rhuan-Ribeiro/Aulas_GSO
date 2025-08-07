# Aula: Configurando IP Fixo no Ubuntu Server

Nesta aula, vamos aprender como configurar um **IP fixo (estático)** no Ubuntu Server. Entenderemos também o que são **interfaces de rede**, o que é um **IP dinâmico**, como funciona o **DHCP**, e como usar o editor de texto **Vim**.

---

## Conceitos importantes

### O que é uma Interface de Rede?
A **interface de rede** é a conexão entre o sistema operacional e a rede, podendo ser uma placa de rede física (como a `enp0s3`) ou virtual. Cada interface pode ter um IP configurado.

### IP Dinâmico vs IP Estático
- **IP Dinâmico**: atribuído automaticamente por um servidor DHCP (como o do seu roteador). Pode mudar após reiniciar o sistema.
- **IP Estático (Fixo)**: atribuído manualmente. Não muda, o que é útil para servidores, impressoras e outros dispositivos que precisam ser sempre acessíveis no mesmo endereço.

### O que é DHCP?
**DHCP (Dynamic Host Configuration Protocol)** é um protocolo que automaticamente fornece um endereço IP, gateway, DNS, etc., para dispositivos na rede.

### O que é o Vim?
**Vim** é um editor de texto usado em ambientes Linux, especialmente em servidores, onde interfaces gráficas não estão disponíveis. Para sair do Vim:
- `Esc` + `:q` → Sair sem salvar
- `Esc` + `:wq` → Salvar e sair
- `Esc` + `:q!` → Forçar saída sem salvar

---

## 1. Verificando Interfaces de Rede

Use o comando abaixo para visualizar as interfaces ativas:

```bash
ifconfig
```

Se quiser ver todas as interfaces, inclusive as inativas:

```bash
ifconfig -a
```

Para ver o gateway padrão da rede, use:

```bash
ip route
```

---

## 2. Verificar se o IP desejado está disponível

Antes de configurar um IP fixo, é fundamental verificar se ele está livre. Se dois dispositivos tiverem o mesmo IP, ocorrerão conflitos de rede.

Exemplo de verificação com **ping**:

```bash
ping 192.168.15.10
```
> Se houver resposta, o IP já está em uso. Escolha outro.

---

## 3. Parar a interface de rede antes da alteração

É importante parar a interface antes de fazer alterações:

### Verificando o Status da Rede:
```bash
systemctl status networking.service
```

---

### Parando a interface da rede:
```bash
ifdown enp0s3
```
> Substitua **enp0s3** pelo nome da sua interface.

---

## 4. Editar o arquivo de configuração da interface

Vamos usar o Vim para editar a configuração da interface de rede:

```bash
vim /etc/network/interfaces.d/enp0s3
```
> Se o arquivo não existir, você pode criá-lo.

### Exemplo de configuração estática:

Altere (ou adicione) as linhas do arquivo:

```bash
auto enp0s3
iface enp0s3 inet static
    address 192.168.15.10
    netmask 255.255.255.0
    gateway 192.168.15.1
```

---

## 5. Subir a interface novamente

Depois de salvar o arquivo, ative a interface:

```bash
ifup enp0s3
```

---

## 6. Reiniciar o serviço de rede

Reinicie o serviço de rede para aplicar as mudanças:

```bash
systemctl restart networking.service
```

Verifique se está ativo:

```bash
systemctl status networking.service
```

---

## 7. Confirmar se o IP foi atribuído

Use o comando novamente para verificar:

```bash
ifconfig -a
```

Se tudo estiver correto, o IP fixo será exibido. Caso o ip não tenha mudado para o que configuramos, talvez seja necessário reiniciar o sistema:

```bash
reboot
```

---

## Resumo das etapas

1. Verifique a interface com ifconfig
2. Pingue o IP desejado
3. Pare a interface com ifdown
4. Edite a configuração com vim
5. Altere para IP estático e salve
6. Suba a interface com ifup
7. Reinicie o serviço com systemctl restart
8. Verifique e, se necessário, reinicie o sistema

