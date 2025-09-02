# Research Bot – Digest Diário de Ações (B3)

Um robô em Python que coleta notícias, relatórios de casas de análise e opiniões de fóruns de investidores sobre empresas da **B3**, processa essas informações com **IA**, e gera um **relatório diário por e-mail** (seg–sex, 08:00 BRT) com análises consolidadas.

## 📌 Visão Geral

O objetivo é oferecer uma forma simples de acompanhar empresas da B3 com base em múltiplas fontes:

- **Portais de notícia**: Valor Econômico, InfoMoney, Exame, O Globo.  
- **Casas de análise**: XP, Genial, BTG Pactual, Empiricus, Bradesco BBI.  
- **Fóruns de investidores**: Investidor10, InfoMoney Clubs, Guiainvest.  

O relatório final contém:

- Resumo **global** (impactos positivos/negativos/neutros por empresa e total do dia).  
- **Seção por empresa** com:  
  - Nota consolidada (curto, médio e longo prazo).  
  - Posição do dia (compra, manter ou venda).  
  - Preço-alvo do dia (com base em analistas ou consenso do dia).  
  - Tabela de notícias e relatórios com resumo explicativo.  
- Rodapé com aviso: *conteúdo gerado por IA, não constitui recomendação financeira profissional*.  

---

## ⚙️ Estrutura do Projeto

research-bot/
├─ app.py # Orquestrador: roda pipeline e dispara digest
├─ settings.py # Configurações globais (limites, domínios, e-mail)
├─ companies/ # Arquivos YAML por empresa
│ ├─ PETR4.yaml
│ └─ VALE3.yaml
├─ api_ia/ # Cliente IA (OpenAI por padrão, trocável)
│ └─ openai_client.py
├─ fetchers/ # Coleta de links
│ ├─ google_news.py
│ └─ manual_links.py
├─ processors/ # Extração de texto e análise
│ ├─ extract.py
│ └─ analyze.py
├─ reporters/ # Construção do relatório e envio
│ ├─ build_html.py
│ └─ emailer.py
├─ storage/ # Histórico e cache
│ ├─ history.sqlite (opcional)
│ └─ seen_links.json
├─ data/
│ └─ logs/
└─ LICENSE

yaml
Copiar código

---

## 🚀 Como Funciona

1. **Configuração da empresa** em `companies/<TICKER>.yaml`:
   ```yaml
   nome: Petrobras
   ticker: PETR4
   ativo: true
   acompanhando: true
   termos: [PETR4, PETR3, Petrobras]
   fazer_busca_auto: true
   links_manuais: []
   limites:
     max_links_total: 10
     dedup_ttl_dias: 3
Coleta: busca notícias recentes em fóruns, casas de análise e portais, além de links manuais.

Processamento: extrai texto, classifica a fonte e envia para a IA analisar.

Análise por IA: gera impacto, recomendação, preço-alvo e resumo explicativo.

Relatório diário: consolida os dados em um digest único e envia por e-mail.

Histórico opcional: salva análises em CSV/SQLite apenas para empresas em acompanhamento.

🛠️ Requisitos
Python 3.10+

Dependências:

bash
Copiar código
pip install -r requirements.txt
Conta de e-mail (ex.: Gmail com App Password).

API Key da OpenAI (ou outro provedor de IA).

🔑 Configuração
Copie o .env.example para .env e configure:

env
Copiar código
OPENAI_API_KEY=sua_chave_aqui
GMAIL_USER=seuemail@gmail.com
GMAIL_APP_PASSWORD=sua_senha_app
TO_EMAIL=destinatario@gmail.com
TIMEZONE=America/Sao_Paulo
Edite os arquivos YAML em companies/ para definir as empresas que quer acompanhar.

Teste o app localmente:

bash
Copiar código
python app.py --mode digest
📬 Agendamento
Para rodar automaticamente todos os dias úteis às 08:00 BRT:

Linux/macOS (cron):

bash
Copiar código
0 8 * * 1-5 /usr/bin/python3 /caminho/app.py --mode digest
Windows (Agendador de Tarefas):
Configure uma tarefa para executar python app.py --mode digest em dias úteis às 08:00.

⚠️ Aviso
Este projeto é experimental e utiliza IA para gerar análises.
Não constitui recomendação de investimento profissional.
Use por sua conta e risco.

📄 Licença
Este projeto está licenciado sob a MIT License – © 2025 Renan Azevedo

yaml
Copiar código

---

Quer que eu adapte esse **README** para um estilo mais “profissional/corporativo” (parecido com documentação de produto), ou prefere manter esse tom mais **open source de dev**?







Perguntar ao ChatGPT

