# Projeto Integrador

**1. Identificação da Equipe e Links**

Nome Completo | Matrícula | Usuário GitHub (@) | Papel Principal no Time 

Marcus Vinicius | [Matrícula] | @usuario1 | Product Owner (PO) 
Laura Nicole | [Matrícula] | @usuario2 | Scrum Master (SM) 
Davi Pereira | [Matrícula] | @usuario3 | Desenvolvedor / Equipe Técnica 
Matheus Felipe | [Matrícula] | @Matheu4Felipe | Desenvolvedor / Equipe Técnica 
Márcio Araújo | [Matrícula] | @usuario5 | Desenvolvedor / Equipe Técnica 

* **Link do Repositório GitHub:** `https://github.com/Matheu4Felipe/Projeto-Integrador`

---

## 2. Fundamentação e Dinâmica dos Papéis Ágeis

### A) Product Owner (PO)
1. **Quem é o PO da equipe?** Marcus Vinicius.
2. **Atribuições e Responsabilidades:** Detém o domínio das regras de negócio tributárias da SEFIN, prioriza o Backlog com foco na otimização da arrecadação e no IPTU Social, faz a interface com o professor/cliente e valida se os entregáveis cumprem os critérios de aceite.
3. **Validação das Entregas:** Validará se as funcionalidades cumprem o propósito através da verificação dos critérios de aceite de cada requisito funcional e da conferência dos relatórios gerados.

### B) Scrum Master (SM)
1. **Quem é o Scrum Master da equipe?** Laura Nicole.
2. **Atribuições e Responsabilidades:** Garante a aplicação das práticas ágeis, remove impedimentos técnicos e organizacionais, facilita os ritos da equipe e assegura que todos os integrantes colaborem no versionamento do projeto.
3. **Comunicação e Alinhamentos:**
   * **Canal Oficial:** WhatsApp (comunicação rápida) e Google Meet/Discord (reuniões).
   * **Frequência:** Alinhamentos assíncronos diários e reunião síncrona semanal.

---

## 3. Especificação de Requisitos Funcionais (RF)

| ID | Nome do Requisito | Descrição / História de Usuário | Critérios de Aceite (Validação) |
| :--- | :--- | :--- | :--- |
| **RF01** | Visualizar Dívidas Consolidadas | Como **Procurador**, quero ver todas as dívidas do contribuinte juntas na tela, para analisar o histórico sem abrir processo por processo. | 1. Exibir 100% dos débitos cadastrados até o dia anterior.<br>2. Agrupar débitos por CPF/CNPJ em uma única visão. |
| **RF02** | Filtrar e Excluir IPTU Social | Como **Analista**, quero filtrar a base de contribuintes por faixa de renda para identificar e excluir automaticamente os beneficiários do IPTU Social da cobrança. | 1. Consultar renda via API da prefeitura.<br>2. Marcar elegíveis (`isIptuSocial=True`) e mover para base de isenção.<br>3. Retirar 100% dos beneficiários das listas automáticas de cobrança. |
| **RF03** | Exportar Ranking em PDF | Como **Analista**, quero exportar o ranking de recuperação da dívida ativa em PDF para instruir os processos administrativos. | 1. Gerar arquivo `ranking_recuperacao.pdf` com link para download na interface.<br>2. Incluir ordenação por probabilidade/chance de pagamento. |
| **RF04** | Consultar Débitos e Emitir Guia | Como **Cidadão**, quero consultar meus débitos pelo CPF/CNPJ para emitir a guia de pagamento direto. | 1. Permitir consulta simples via CPF em até 3 cliques sem cadastro prévio.<br>2. Gerar guia de pagamento integrada à API da prefeitura. |
| **RF05** | Relatório de Arrecadação | Como **Secretário**, quero visualizar o relatório mensal de arrecadação de IPTU/ISS para acompanhar a meta sem pedir relatórios manuais. | 1. Exibir dados consolidados mensais de arrecadação.<br>2. Atualizar indicadores de meta automaticamente. |
| **RF06** | Exportação de Dados em CSV | O sistema deve permitir que o analista exporte a lista de contribuintes ordenados em formato CSV. | 1. Gerar arquivo em formato de texto simples `.csv` com estrutura de tabela legível. |
| **RF07** | Autenticação para Acesso a Dados | O sistema deve controlar o acesso aos dados dos contribuintes mediante autenticação. | 1. Permitir acesso ao banco/interface do analista e procurador somente após autenticação (suporte ao Gov.br). |
| **RF08** | Registro de Logs e Auditoria | O sistema deve manter registro auditável de todas as consultas efetuadas. | 1. Gravar em log a data, hora e ID do usuário para 100% das consultas realizadas. |
| **RF09** | Classificação por Grupos de Renda | O sistema deve agrupar contribuintes por similaridade de IPTU e ISS para identificar padrões de pagamento. | 1. Agrupar pagantes de forma anônima por faixa de renda/similaridade.<br>2. Calcular porcentagem e variação da taxa de pagamento de cada grupo. |
| **RF10** | Modelo Preditivo de Recuperação | O modelo de IA deve estimar a chance de pagamento das dívidas ativas para ordenar a prioridade de cobrança. | 1. Atingir no mínimo 75% de precisão na classificação dos devedores. |

---

## 4. Requisitos Não Funcionais (RNF)

| ID | Categoria | Descrição da Restrição | Métrica / Forma de Teste |
| :--- | :--- | :--- | :--- |
| **RNF01** | Desempenho | O sistema deve responder às consultas de débitos e filtros com rapidez. | Responder às consultas em até 3 segundos em 95% dos casos. |
| **RNF02** | Explicabilidade / IA | O sistema deve mostrar os motivos que definiram a chance de pagamento da dívida. | Exibir justificativa lógica do cálculo de pontuação cumprindo regras da LGPD. |
| **RNF03** | Privacidade e Segurança (LGPD) | O ambiente de análise deve proteger dados pessoais e utilizar conexão segura. | NENHUM dado que identifique o contribuinte é armazenado no ambiente de análise; exigir conexão HTTPS para a API. |
| **RNF04** | Proteção Social | O pipeline de automação deve impedir a cobrança indevida de isentos. | Garantir que 100% dos beneficiários do IPTU Social sejam removidos da lista automática de cobrança. |
| **RNF05** | Portabilidade e Setup | As dependências do projeto devem estar isoladas e descritas em arquivo de manifesto em Python. | Instalação e execução com comando padrão via `requirements.txt` / `pyproject.toml` em Python 3.12+. |

---

## 5. Matriz de Priorização MoSCoW

* **Must Have (Indispensável para o MVP):** `RF01` (Visualizar Dívidas Consolidadas), `RF02` (Filtrar IPTU Social) e `RNF03` (Privacidade/LGPD).
* **Should Have (Importante, alta prioridade):** `RF04` (Consulta/Guia Cidadão), `RF05` (Relatório Secretário), `RF07` (Autenticação) e `RNF01` (Desempenho).
* **Could Have (Desejável, se houver tempo hábil):** `RF03` (Exportar Ranking PDF), `RF06` (Exportação CSV) e `RF09` (Classificação Anônima).
* **Won't Have (Fora do escopo desta entrega):** Notificações e alertas automáticos por mensagem aos contribuintes (adiados para focar no modelo de IA e integração dos dados da prefeitura).

---

## 6. Comprovação de Contribuições no Git

*(Adicione as capturas de tela dentro da pasta `docs/prints_git/` do repositório)*

1. **Painel de Contribuidores:** `![Contributors](docs/prints_git/contributors.png)`
2. **Histórico de Commits:** `![Commits](docs/prints_git/commits.png)`

---

## 7. Documentação Complementar e Modelagem UML (Bônus +10%)

A documentação visual desenvolvida na oficina da disciplina está anexada na pasta `docs/uml/`:
* **Diagrama 1 - Casos de Uso:** Mapeamento de interações (Procurador, Analista, Cidadão, Secretário e API).
* **Diagrama 2 - Diagrama de Classes:** Estruturas de entidade e controle do sistema de Dívida Ativa.
* **Diagrama 3 - Diagrama de Sequência:** Processo de filtro, consulta de renda e concessão de IPTU Social.
  1. Agrupar pagantes de forma anônima por faixa de renda/similaridade.<br>2. Calcular porcentagem e variação da taxa de pagamento de cada grupo.
  
**RF10**: Modelo Preditivo de Recuperação o modelo de IA deve estimar a chance de pagamento das dívidas ativas para ordenar a prioridade de cobrança. 
  1. Atingir no mínimo 95% de precisão na classificação dos devedores.
