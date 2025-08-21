# Introdução a Sistemas Operacionais de Servidores (31/07/2025)

## 1. Diferença entre Sistemas Desktop e Servidor

### Conceito

**Desktop:** Sistema projetado para uso pessoal, com foco em usabilidade e interface gráfica amigável (ex: Windows 11, Ubuntu Desktop).

**Servidor:** Sistema projetado para alta disponibilidade, confiabilidade, gerenciamento de serviços e multiusuário (ex: Windows Server, Ubuntu Server).

### Comparação

| Característica       | Desktop                    | Servidor                          |
|----------------------|----------------------------|-----------------------------------|
| Interface            | Gráfica (GUI)              | Geralmente CLI                    |
| Prioridade           | Experiência do usuário     | Desempenho e estabilidade         |
| Serviços ativos      | Diversos apps e recursos   | Serviços específicos (web, DNS)   |
| Multitarefa pesada   | Limitada                   | Projetado para isso               |
| Exemplo              | Windows 10, Ubuntu Desktop | Debian Server, Windows Server     |

> "Um servidor não precisa ser bonito, precisa funcionar 24/7."

---

## 2. Linux Server vs Windows Server

### Linux Server

- Distribuições comuns: Ubuntu Server, Debian, CentOS, Rocky Linux.
- Open Source (código aberto).
- Mais leve, altamente configurável.
- CLI por padrão.
- Comunidade ativa.
- Licença gratuita.

### Windows Server

- GUI por padrão (mas suporta PowerShell e CLI).
- Licença paga.
- Integração com Active Directory, Hyper-V, IIS.
- Gerenciamento facilitado com ferramentas como Server Manager.

### Tabela Comparativa

| Característica      | Linux Server              | Windows Server                    |
|---------------------|---------------------------|-----------------------------------|
| Custo               | Gratuito (em geral)       | Pago/licenciado                   |
| Interface padrão    | CLI                       | GUI                               |
| Suporte             | Comunidade / Profissional | Profissional (MSDN, TechNet)      |
| Segurança           | Configuração manual, menos alvo | Patches regulares, alvo comum |
| Customização        | Alta                      | Limitada                          |

> Demonstração sugerida: Abrir uma VM com Ubuntu Server (sem GUI) e outra com Windows Server 2019. Mostrar login via terminal no Ubuntu e via interface no Windows.

---

## 3. Tipos de Interface: CLI vs GUI

### CLI (Command Line Interface)

- Leve, rápida e poderosa.
- Exige familiaridade com comandos.
- Exemplo: `sudo apt install nginx` no Linux.

### GUI (Graphical User Interface)

- Visual, intuitiva.
- Ocupa mais recursos.
- Mais usada em sistemas desktop ou em servidores de pequenas empresas.

### Comparação

| Interface | Vantagens                  | Desvantagens                 |
|-----------|----------------------------|------------------------------|
| CLI       | Rápida, leve, scriptável   | Curva de aprendizado maior   |
| GUI       | Intuitiva, acessível       | Mais consumo de recursos     |

> Atividade: Faça os alunos abrirem um terminal e rodar comandos simples como `ls`, `pwd`, `ip a`, `hostname`.

---

## 4. Vantagens e Limitações das Arquiteturas de Servidores

### Estabilidade

- **Linux:** reconhecido por uptimes altos.
- **Windows Server:** melhorou muito, mas reinicializações mais comuns.

### Desempenho

- **Linux:** mais leve por padrão, ideal para servidores web.
- **Windows Server:** GUI e serviços aumentam uso de RAM e CPU.

### Licença

- **Linux:** gratuito.
- **Windows Server:** custo de licença + CALs.

### Suporte

- **Linux:** comunidade e empresas (Canonical, Red Hat).
- **Windows Server:** Microsoft, planos de suporte empresarial.

### Segurança

- **Linux:** filosofia de permissões mais restritiva, muitos recursos de firewall e hardening.
- **Windows Server:** sistema de atualizações mais automatizado e políticas de segurança integradas.

