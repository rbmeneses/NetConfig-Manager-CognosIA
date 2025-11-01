# NetConfig Manager

Gerenciador centralizado de inventário, backup de configurações de switches e visualização de topologia de rede com Streamlit.

## 📌 Funcionalidades

- Inventário de dispositivos em **SQLite**
- Backup automático via **SSH (Paramiko)**
- Detecção de mudanças com **Diff** e alerta por e-mail
- Mapa mental de ferramentas (Graphviz)
- Topologia interativa com **streamlit-agraph** e ícones
- Geração de configuração base para switches:
  - Cisco IOS
  - Huawei VRP
  - Juniper JunOS
  - Aruba AOS-CX
- Exportação de resultados e logs

## 🧰 Tecnologias

| Componente | Uso |
|-----------|-----|
| Streamlit | Interface Web |
| SQLite | Inventário |
| Paramiko | SSH para coleta de configs |
| Graphviz | Mapa de ferramentas |
| streamlit-agraph | Topologia interativa |
| Requests + Gemini API | Análises com IA |
| SMTP | Alertas por e-mail |

---

## 🚀 Instalação

```bash
git clone https://github.com/rbmeneses/NetConfig-Manager.git
cd NetConfig-Manager
