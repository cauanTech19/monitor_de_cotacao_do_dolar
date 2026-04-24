# 📊 Monitor de Cotação do Dólar

Pipeline de automação em Python que coleta a cotação do dólar em tempo real, gera um relatório Excel formatado com gráfico de tendência e envia um resumo automático por email.

---

## 🚀 O que o projeto faz

1. **Coleta** a cotação atual do dólar via [AwesomeAPI](https://docs.awesomeapi.com.br/)
2. **Persiste** o histórico das últimas 30 cotações em JSON
3. **Processa** os dados com pandas (média, máxima, mínima, tendência)
4. **Gera** um relatório `.xlsx` formatado com duas abas e gráfico de linha
5. **Notifica** via Gmail com um resumo completo automaticamente

---

## 🛠️ Tecnologias utilizadas

| Biblioteca | Uso |
|---|---|
| `requests` | Consumo da API de cotações |
| `pandas` | Transformação e análise dos dados históricos |
| `openpyxl` | Geração e formatação do relatório Excel |
| `smtplib` | Envio de email via Gmail (biblioteca nativa do Python) |
| `schedule` | Agendamento da execução automática |

---

## 📁 Estrutura do projeto

```
monitor-dolar/
├── message.py              # Script principal com o pipeline completo
├── historico.example.json  # Exemplo do formato do histórico
├── .gitignore
└── README.md
```

> **Nota:** `historico.json` e `relatorio.xlsx` são gerados automaticamente na primeira execução e estão no `.gitignore`. Use `historico.example.json` como referência do formato esperado.

---

## ⚙️ Como configurar

### 1. Clone o repositório

```bash
git clone https://github.com/cauanTech19/monitor_de_cotacao_do_dolar.git
cd monitor_de_cotacao_do_dolar
```

### 2. Instale as dependências

```bash
pip install requests pandas openpyxl schedule
```

> `smtplib` já vem instalado com o Python — nenhuma instalação extra necessária.

### 3. Gere a senha de app do Gmail

1. Acesse [myaccount.google.com](https://myaccount.google.com)
2. Segurança → **Verificação em duas etapas** (precisa estar ativa)
3. Pesquise **"Senhas de app"** na barra de busca da conta
4. Crie uma senha para **Outro (nome personalizado)** → coloque `monitor-dolar`
5. O Google gera uma senha de 16 caracteres — guarde ela para o próximo passo

> A senha de app é diferente da sua senha normal do Gmail e serve exclusivamente para este projeto.

### 4. Configure as variáveis no script

Abra o `message.py` e edite as constantes no topo do arquivo:

```python
EMAIL_REMETENTE:    str = "seuemail@gmail.com"
EMAIL_DESTINATARIO: str = "seuemail@gmail.com"  # pode ser outro email se quiser
EMAIL_SENHA_APP:    str = "sua_senha_de_app"     # senha de 16 caracteres gerada no passo anterior
LIMITE_DOLAR:       float = 5.80                 # valor que dispara o alerta 🚨
```

---

## ▶️ Como executar

### Execução manual

```bash
python message.py
```

Na primeira execução o script já busca a cotação, salva o histórico, gera o Excel e envia o email.

### Agendamento automático (Windows)

Para rodar automaticamente sem deixar o terminal aberto, use o **Agendador de Tarefas do Windows**:

1. Abra o **Agendador de Tarefas** (pesquise na barra do Windows)
2. Clique em **Criar Tarefa Básica**
3. Defina o gatilho: **Diariamente** nos horários que preferir (ex: 9h e 18h)
4. Ação: **Iniciar um programa**
   - Programa: caminho do Python (descubra com `where python` no terminal)
   - Argumentos: caminho completo do `message.py`
5. Salve e pronto — o Windows dispara o script automaticamente

---

## 📬 Exemplo de email recebido

```
Assunto: 📊 Relatório Dólar

📊 Relatório Dólar — 23/04/2026 18:00
━━━━━━━━━━━━━━
Agora:     R$ 5.03  ✅ Dentro do Normal
Média:     R$ 5.05
Máxima:    R$ 5.12
Mínima:    R$ 4.98
Tendência: Baixa 📉
━━━━━━━━━━━━━━
Relatório Excel gerado automaticamente.
```

---

## 📈 Relatório Excel gerado

O arquivo `relatorio.xlsx` contém duas abas:

- **Historico** — série completa de cotações com gráfico de linha
- **Resumo** — tabela com as métricas calculadas do período

---

## 🔭 Próximos passos

- [ ] Monitorar outras moedas (EUR, BTC, ARS)
- [ ] Adicionar análise de tendência com IA (Claude API)
- [ ] Enviar o arquivo Excel como anexo no email
- [ ] Deploy em servidor cloud para rodar 24/7

---

## 📄 Licença

MIT — sinta-se livre para usar, modificar e distribuir.

