
# PharmaIA_Alert

## Squad 5

### Integrantes

* Marcos Vinicius de Lucena - 1282515264
* Rafael Bulhões Emerenciano -12825128576
* Iury Thierry - 12825137136
* Yan Gustavo 12825135945
* Jardson Ribeiro Costa- 12825132136
* Richard Ryan 12826125846


---

# Sobre o Projeto

O PharmaIA_Alert é um agente inteligente desenvolvido para automatizar a comunicação entre farmácias e clientes que aguardam a disponibilidade de medicamentos.

O sistema monitora o estoque automaticamente, identifica clientes interessados em medicamentos específicos e realiza notificações personalizadas por e-mail quando o produto solicitado está disponível.

A solução utiliza Inteligência Artificial para analisar informações de estoque, tomar decisões de forma autônoma e executar ações sem intervenção humana.

---

# Problema

Muitas farmácias realizam o acompanhamento de medicamentos indisponíveis de forma manual, exigindo consultas frequentes por parte dos clientes e aumentando o tempo gasto pelos atendentes.

O PharmaIA_Alert automatiza esse processo, reduzindo o tempo de resposta e melhorando a experiência do cliente.

---

# Objetivo

Desenvolver um agente inteligente capaz de:

* Consultar dados de estoque.
* Identificar clientes aguardando medicamentos.
* Analisar a disponibilidade dos produtos.
* Gerar mensagens personalizadas.
* Enviar notificações automaticamente.
* Registrar todas as ações realizadas.

---

# Instruções para importar e executar o workflow

1. Acesse sua conta no n8n.
2. Clique em **Import workflow**.
3. Selecione o arquivo `PharmaIA_Alert.json`.
4. Após importar, configure as credenciais necessárias:
   - Google Sheets OAuth2
   - Gmail OAuth2
   - OpenRouter API
   - Google Gemini API
5. Crie ou vincule uma planilha Google chamada `PharmaIA_Alert`.
6. A planilha deve conter as abas:
link da planilha: https://docs.google.com/spreadsheets/d/1O0il2zBV-4O81t5bb30GXcmTa_PMVhbJCcSjvnHWTJU/edit?gid=0#gid=0
   - `Estoque`
   - `Clientes_Interessados`
   - `Log_Notificacoes`
7. Confira se as colunas seguem o padrão esperado:
   - Estoque: `Medicamento`, `Quantidade`
   - Clientes_Interessados: `Cliente`, `Telefone`, `Email`, `Medicamento`, `Status`
   - Log_Notificacoes: `Cliente`, `Medicamento`, `Data`, `Status`, `Mensagem`, `Motivo`
8. No n8n, atualize os nós do Google Sheets para apontarem para a sua planilha.
9. Execute o workflow manualmente para teste ou ative o `Schedule Trigger` para execução automática.

# Variáveis e credenciais necessárias

```env
GOOGLE_SHEETS_CREDENTIAL=SUA_CREDENCIAL_GOOGLE_SHEETS_AQUI
GMAIL_CREDENTIAL=SUA_CREDENCIAL_GMAIL_AQUI
OPENROUTER_API_KEY=SUA_CHAVE_OPENROUTER_AQUI
GEMINI_API_KEY=SUA_CHAVE_GEMINI_AQUI
```

---

# Arquitetura da Solução

O sistema foi desenvolvido utilizando a plataforma n8n para orquestração dos fluxos de automação.

Fluxo principal:

1. Execução automática através de agendamento.
2. Consulta do estoque via Google Sheets.
3. Consulta dos clientes interessados.
4. Análise realizada por Inteligência Artificial.
5. Verificação das condições de notificação.
6. Envio automático de e-mail.
7. Atualização do status do cliente.
8. Registro de auditoria das notificações.
9. Registro de falhas e notificações ignoradas.

---

# Armazenamento dos Dados

O PharmaIA Alert utiliza o Google Sheets como solução de armazenamento de dados durante a fase de prototipação e desenvolvimento acadêmico.

As informações são organizadas em diferentes abas da planilha:

## Estoque

Armazena os medicamentos disponíveis e suas respectivas quantidades.

## Clientes_Interessados

Armazena os clientes que desejam ser notificados quando um medicamento voltar a estar disponível, incluindo dados como, telefone, email, medicamento e o satus.

## Log_Notificacoes

Armazena o histórico de notificações enviadas pelo sistema, incluindo cliente, medicamento, data e status da operação.

# Justificativa da Escolha

O Google Sheets foi escolhido por apresentar:

- Fácil integração com o n8n;
- Simplicidade de configuração;
- Baixo custo de implementação;
- Facilidade de visualização dos dados;
- Adequação ao escopo acadêmico do projeto.

# Segurança e Privacidade

O acesso às planilhas é controlado por permissões da conta Google utilizada no projeto.

O sistema armazena apenas os dados mínimos necessários para funcionamento da solução, como:

- Nome do cliente;
- E-mail;
- Medicamento solicitado;
- Status da solicitação.

Nenhuma credencial, chave de API ou informação sensível é armazenada no repositório GitHub.

# Evolução Futura

Em um ambiente de produção, o Google Sheets poderá ser substituído por soluções mais robustas de armazenamento, como PostgreSQL, MySQL ou Firebase, oferecendo maior escalabilidade, desempenho e controle de acesso.

---

# Funcionamento do Agente

## Percepção

O agente coleta informações de:

* Estoque de medicamentos.
* Lista de clientes interessados.
* Status atual das solicitações.

## Raciocínio

A Inteligência Artificial analisa:

* Se o medicamento solicitado está disponível.
* Se o cliente está com status "Aguardando".
* Se a notificação deve ser enviada.

## Ação

O agente:

* Gera mensagens personalizadas.
* Envia notificações por e-mail.
* Atualiza registros na base de dados.
* Armazena logs de auditoria.

---

# Fallback de Inteligência Artificial

Para aumentar a disponibilidade e a resiliência do sistema, foi implementado um mecanismo de fallback entre provedores de IA.

Fluxo de execução:

1. O sistema utiliza o OpenRouter como provedor principal.
2. Caso ocorra falha na execução ou indisponibilidade do serviço, o fluxo redireciona automaticamente para o Google Gemini.
3. O processo continua sem interrupção para o usuário final.

Essa abordagem garante maior confiabilidade e continuidade operacional.

---

# Tecnologias Utilizadas

* n8n
* Google Sheets
* Gmail API
* OpenRouter
* Google Gemini
* Inteligência Artificial Generativa

---

# Auditoria e Rastreabilidade

Todas as execuções são registradas na planilha de logs contendo:

* Cliente
* Medicamento
* Data
* Status
* Mensagem enviada
* Motivo da decisão

Isso permite auditoria completa das notificações realizadas pelo sistema.

---

# Privacidade e LGPD

O sistema utiliza apenas os seguintes dados:

* Nome
* E-mail
* Medicamento solicitado

Os dados são utilizados exclusivamente para notificação de disponibilidade de medicamentos.

Nenhuma informação é compartilhada com terceiros e o tratamento dos dados é realizado apenas para a finalidade prevista pelo sistema.

# Boas práticas adotadas

- Coleta apenas dos dados mínimos necessários para o funcionamento do serviço.
- Utilização dos dados exclusivamente para comunicação com o cliente.
- Não armazenamento de informações sensíveis de saúde, receitas médicas ou dados financeiros.
- Possibilidade de remoção dos dados do cliente mediante solicitação.

# Conformidade com a LGPD

- Finalidade: uso dos dados apenas para notificação de medicamentos.
- Necessidade: coleta apenas das informações essenciais.
- Transparência: o cliente sabe quais dados são armazenados e para qual finalidade.
- Segurança: credenciais e chaves de acesso não são expostas publicamente.

---

# Resultados Esperados

* Redução do trabalho manual da farmácia.
* Maior rapidez na comunicação com clientes.
* Melhor controle das solicitações de medicamentos.
* Aumento da eficiência operacional.
* Automatização do processo de notificação.

---

# Demonstração do Fluxo

Agendamento → Consulta de Estoque → Consulta de Clientes → IA → Validação → Notificação → Atualização de Status → Auditoria
