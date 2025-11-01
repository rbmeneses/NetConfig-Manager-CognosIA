# 🚀 NetConfig Manager

Uma suíte de automação de rede completa, construída com Streamlit e IA, para gerenciar, auditar e configurar sua infraestrutura de rede de forma visual e inteligente.

`[ADICIONAR IMAGEM: Banner ou GIF principal do App em Ação]`

## 📖 Sobre o Projeto

O **NetConfig Manager** é uma ferramenta de UI web projetada para centralizar as tarefas mais comuns de um engenheiro de redes. Ele combina automação de SSH (via Paramiko), um inventário persistente (SQLite) e o poder da IA generativa (Google Gemini) para oferecer uma solução robusta que vai além de simples scripts.

O objetivo é automatizar o backup de configurações, auditar a segurança, visualizar topologias complexas e até mesmo gerar novos scripts de configuração de dispositivos, tudo a partir de uma interface amigável.

## ✨ Funcionalidades Principais

O arsenal de ferramentas do NetConfig Manager inclui:

* **📦 Backup Automatizado de Rede:**
    * Conecta-se via SSH a múltiplos dispositivos (Cisco, Huawei, Juniper, etc.) em paralelo.
    * Salva backups de configuração em disco de forma organizada.
    * **Detecta Mudanças (Diff):** Compara o backup mais recente com o anterior e exibe um "diff" visual.
    * **Alertas por E-mail:** Envia alertas via SMTP caso uma mudança de configuração seja detectada ou um backup falhe.

* **🗂️ Gerenciador de Inventário (SQLite):**
    * Banco de dados centralizado para todos os ativos de rede.
    * Interface CRUD (Adicionar, Editar, Remover) completa.
    * Armazena metadados essenciais, como IP, vendor, local e, crucialmente, **dados de topologia (quem se conecta a quem)**.

* **🌐 Visualização de Topologia Interativa:**
    * Renderiza um diagrama de rede interativo (com zoom e pan) usando os dados de `switch_pai` e `porta_pai` do inventário.
    * Utiliza ícones personalizados (switch, roteador, firewall) para uma visualização clara.
    * Permite filtrar a topologia a partir de um nó "raiz" específico.

* **🤖 Assistente de Configuração (ConfigGenius v2):**
    * Um assistente passo-a-passo (7 etapas) para gerar scripts de configuração "best-practice" do zero.
    * Inclui configuração de sistema, usuários, gerenciamento, AAA, SNMP, Syslog, Port Security e QoS.
    * Utiliza templates otimizados para **Cisco (IOS), Huawei (VRP), Juniper (Junos) e Aruba (AOS-CX)**.
    * Permite baixar o script gerado como `.txt`.

* **🛡️ Auditor de Configuração (com IA):**
    * Utiliza a **API do Gemini** para analisar um arquivo de backup de configuração.
    * Procura por falhas graves de segurança, más práticas e configurações ausentes (NTP, logging, banners).
    * Fornece um sumário executivo, uma nota de 0 a 10 e recomendações acionáveis.

* **⚡ Executor de Comandos em Massa:**
    * Permite enviar comandos de visualização (`show`, `display`) para múltiplos dispositivos do inventário de uma só vez.
    * Agrega os resultados em um único painel para análise rápida.

* **💡 Central de Ajuda (com IA):**
    * Um guia de ajuda dinâmico onde o usuário pode perguntar sobre qualquer ferramenta do app, e a **IA Gemini** gera uma explicação detalhada sobre seu propósito e modo de uso.

* **🗺️ Mapa de Ferramentas (Alto Nível):**
    * Gera um mapa mental estático (Graphviz) de todos os ativos, agrupados por categoria.

## 📸 Screenshots

`[ADICIONAR IMAGEM: GIF mostrando o fluxo do app, talvez a página de Backup rodando]`

### Topologia de Rede Interativa

`[ADICIONAR IMAGEM: Screenshot da página de Topologia com os nós e ícones personalizados.]`

### Assistente de Geração de Configuração (ConfigGenius v2)

`[ADICIONAR IMAGEM: GIF ou screenshot mostrando o assistente passo-a-passo.]`

### Auditor de Segurança com IA Gemini

`[ADICIONAR IMAGEM: Screenshot do relatório de auditoria gerado pela IA, mostrando as falhas e a nota.]`

### Painel de Backup e Análise de Diff

`[ADICIONAR IMAGEM: Screenshot da página de Backup mostrando o log e um relatório de 'diff' expandido.]`

### Gerenciador de Inventário

`[ADICIONAR IMAGEM: Screenshot da tabela de inventário com o data_editor, mostrando as colunas de topologia.]`

## 🛠️ Tecnologias Utilizadas

* **Backend & Frontend:** Python 3, Streamlit
* **Conectividade de Rede:** Paramiko (SSH)
* **Banco de Dados:** SQLite3
* **Visualização de Dados:** `streamlit-agraph`, Graphviz, Pandas
* **Inteligência Artificial:** Google Gemini API (via `requests`)
* **Configuração:** PyYAML

## ⚙️ Instalação e Configuração

Siga estes passos para executar o projeto localmente:

1.  **Clone o repositório:**
    ```bash
    git clone [https://github.com/seu-usuario/netconfig-manager.git](https://github.com/seu-usuario/netconfig-manager.git)
    cd netconfig-manager
    ```

2.  **Crie um ambiente virtual e instale as dependências:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    pip install -r requirements.txt
    ```
    **Conteúdo do `requirements.txt`:**
    ```plaintext
    streamlit
    pandas
    paramiko
    graphviz
    streamlit-agraph
    requests
    pyyaml
    ```

3.  **Adicione os Ícones da Topologia:**
    Na pasta raiz do projeto, adicione os arquivos de ícone que você está usando (conforme `ICON_PATHS` no script):
    * `icon_switch.png`
    * `icon_firewall.png`
    * `icon_roteador.png`
    * `icon_ap.png`

4.  **Configure suas Chaves e Alertas:**
    Crie um arquivo chamado `config.yaml` na pasta raiz. O aplicativo criará um automaticamente na primeira execução se não o encontrar, mas você pode criá-lo manualmente:
    ```yaml
    api_keys:
      gemini_api_key: 'SUA_CHAVE_DE_API_DO_GEMINI_AQUI'

    smtp:
      enable: false # Mude para true para ativar alertas
      server: 'smtp.office365.com'
      port: 587
      user: 'alertas@suaempresa.com'
      pass: 'SUA_SENHA_DE_EMAIL_AQUI'
      to: 'equipe.redes@suaempresa.com'
    ```

5.  **Execute o aplicativo:**
    ```bash
    streamlit run netconfig_manager2.py
    ```

## 🚀 Como Usar (Fluxo de Trabalho)

1.  **Inventário:** Abra a página **"Gerenciador de Inventário"** e adicione seus dispositivos. Para habilitar a topologia, preencha os campos `switch_pai`, `porta_pai` e `shape` para cada dispositivo.
2.  **Backup:** Vá para **"Backup de Rede"**. Insira suas credenciais SSH na barra lateral, selecione os IPs do inventário e clique em **"Iniciar Novo Backup"**.
3.  **Auditoria:** Após o backup, vá para **"Auditor de Configuração (IA)"**. Os backups da sessão atual aparecerão. Selecione os que deseja analisar e execute a auditoria.
4.  **Visualização:** Confira a **"Visualização de Topologia"** para ver seu diagrama de rede interativo.
5.  **Geração:** Use o **"Assistente de Configuração"** para gerar um novo script de configuração seguro para um novo dispositivo ou para substituir um antigo.

---

## 👤 Autor

* **Ricardo Barbosa de Meneses**
