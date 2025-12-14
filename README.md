# Projeto - Administração de Sistemas Abertos (ASA)

## Descrição do Projeto

Este projeto tem como objetivo principal **simular e automatizar a administração e o provisionamento de uma infraestrutura de múltiplos servidores** utilizando ferramentas de código aberto.

A solução é construída sobre uma estrutura de virtualização usando **Vagrant**, que orquestra a criação de quatro Máquinas Virtuais (VMs) com papéis distintos:
* `arq` (arquitetura/balanceamento)
* `db` (banco de dados)
* `app` (aplicação)
* `cliente` (simulação de acesso)

Toda a configuração e instalação de serviços dentro dessas VMs é realizada de forma automática e idempotente pelo **Ansible**, garantindo um ambiente consistente e replicável.

---

##  Tecnologias Utilizadas

* **Vagrant**: Para o gerenciamento das Máquinas Virtuais.
* **VirtualBox**: Como provedor de virtualização para o Vagrant.
* **Ansible**: Para automação da configuração, instalação de pacotes e provisionamento dos serviços.
* **Shell Script**: Scripts auxiliares para configuração inicial.

---

##  Estrutura do Repositório

O repositório está organizado para facilitar o gerenciamento da Infraestrutura como Código (IaC):

| Diretório/Arquivo | Função |
| :--- | :--- |
| `Vagrantfile` | Define as quatro Máquinas Virtuais (`arq`, `db`, `app`, `cliente`) e as configurações de rede. |
| `ansible.cfg` | Arquivo de configuração principal do Ansible. |
| `hosts.ini` | Inventário do Ansible. Mapeia os hosts virtuais para seus respectivos grupos (ex: `[webservers]`, `[database]`). |
| `playbooks/` | Contém os playbooks (arquivos `.yml`) que definem as tarefas de configuração para cada VM. |
| `.gitignore` | Ignora arquivos gerados automaticamente pela virtualização. |

---

##  Pré-requisitos

Para executar e testar o ambiente, você precisa ter instalado:

1.  **Git** (para clonar o repositório).
2.  **VirtualBox**
3.  **Vagrant**
4.  **Ansible** (facilita a execução manual de playbooks.)

---

##  Autores

Este projeto foi desenvolvido como parte dos requisitos da disciplina de Administração de Sistemas Abertos (ASA).

* Hugo Antônio - Matrícula: 20241380001
* Evandi Francisco - Matrícula: 20241380038
*
