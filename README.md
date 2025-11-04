# Apresentação: Análise de Sistemas - Requisitos e Diagramação de Banco de Dados

---

## Slide 1: **Introdução à Análise de Sistemas**
**O que é Análise de Sistemas?**
- Processo de estudo e compreensão de sistemas existentes ou novos
- Identificação de necessidades e problemas
- Proposta de soluções tecnológicas
- Ponte entre stakeholders e equipe de desenvolvimento

**Objetivo Principal:**
- Entender o que o sistema deve fazer
- Como deve funcionar
- Para quem será desenvolvido

---

## Slide 2: **Importância dos Requisitos**
**Por que os requisitos são cruciais?**
- Base para todo o desenvolvimento
- Evitam retrabalho e custos extras
- Garantem que o sistema atenda às reais necessidades
- Servem como contrato entre cliente e desenvolvedores

**Consequências de requisitos mal definidos:**
- Projetos fora do prazo
- Orçamentos estourados
- Sistemas que não atendem expectativas
- Insatisfação do cliente

---

## Slide 3: **Classificação dos Requisitos**
**Requisitos Funcionais**
- O que o sistema DEVE FAZER
- Funcionalidades específicas
- Exemplo: "O sistema deve permitir login de usuários"

**Requisitos Não-Funcionais**
- Como o sistema DEVE SER
- Qualidades e restrições
- Exemplo: "O sistema deve responder em menos de 2 segundos"

---

## Slide 4: **Técnicas de Levantamento de Requisitos**
**Métodos Comuns:**
- 📋 **Entrevistas**: Diretas com stakeholders
- 👥 **Workshops**: Sessões colaborativas
- 📊 **Questionários**: Coleta em larga escala
- 👀 **Observação**: Análise do processo atual
- 📝 **Análise de Documentos**: Estudo de registros existentes

**Ferramentas:**
- User Stories
- Casos de Uso
- Protótipos

---

## Slide 5: **Especificação de Requisitos**
**Documento de Especificação deve conter:**
- Descrição geral do sistema
- Requisitos funcionais detalhados
- Requisitos não-funcionais
- Regras de negócio
- Restrições técnicas
- Glossário de termos

**Características de bons requisitos:**
- ✅ Completo
- ✅ Consistente
- ✅ Não ambíguo
- ✅ Verificável
- ✅ Rastreável

---

## Slide 6: **Transição: Requisitos → Modelagem de Dados**
**Como os requisitos influenciam o banco de dados?**
- Entidades identificadas nos requisitos
- Relacionamentos descobertos nas regras de negócio
- Atributos definidos pelas funcionalidades
- Restrições derivadas de requisitos não-funcionais

**Exemplo:**
Requisito: "Sistema de biblioteca deve controlar empréstimos de livros"
→ Entidades: Livro, Usuário, Empréstimo

---

## Slide 7: **Introdução à Modelagem de Banco de Dados**
**O que é modelagem de dados?**
- Processo de criação de modelo de dados
- Representação abstrata dos dados
- Define estrutura, relacionamentos e restrições

**Objetivos:**
- Organizar dados de forma eficiente
- Garantir consistência e integridade
- Facilitar manutenção e evolução
- Otimizar performance

---

## Slide 8: **Modelo Entidade-Relacionamento (MER)**
**Componentes Básicos:**
- **Entidades**: "Coisas" sobre quais armazenamos dados
  - Ex: Cliente, Produto, Pedido
- **Atributos**: Características das entidades
  - Ex: Nome, Email, DataNascimento
- **Relacionamentos**: Conexões entre entidades
  - Ex: Cliente FAZ Pedido

---

## Slide 9: **Cardinalidades em Relacionamentos**
**Tipos de Cardinalidade:**
- **1:1** (Um para Um)
  - Ex: Pessoa → CPF
- **1:N** (Um para Muitos)
  - Ex: Departamento → Funcionários
- **N:M** (Muitos para Muitos)
  - Ex: Alunos → Disciplinas

**Notação:**
```
Entidade1 ---(1)--- RELACIONAMENTO ---(N)--- Entidade2
```

---

## Slide 10: **Exemplo Prático: MER - Sistema de Vendas**
```
CLIENTE (1) ----- FAZ ----- (N) PEDIDO (1) ----- CONTÉM ----- (N) PRODUTO
    |                            |                      |
 CPF (PK)                    Número (PK)            Código (PK)
 Nome                        Data                   Descrição
 Email                       Valor                  Preço
 Telefone                    Status                 Estoque
```

**Legenda:**
- PK = Chave Primária
- (1), (N) = Cardinalidades

---

## Slide 11: **Diagrama Entidade-Relacionamento (DER)**
**Ferramentas Populares:**
- MySQL Workbench
- Lucidchart
- Draw.io
- BRModelo
- Enterprise Architect

**Elementos Visuais:**
- Retângulos: Entidades
- Losangos: Relacionamentos
- Elipses: Atributos
- Linhas: Conexões

---

## Slide 12: **Do Modelo Conceitual ao Físico**
**Etapas da Modelagem:**
1. **Modelo Conceitual** (MER/DER) - Alto nível
2. **Modelo Lógico** - Estrutura detalhada
3. **Modelo Físico** - Implementação específica

**Transformação MER → Tabelas:**
- Entidades → Tabelas
- Atributos → Colunas
- Relacionamentos → Chaves estrangeiras
- Cardinalidades → Restrições de integridade

---

## Slide 13: **Normalização de Banco de Dados**
**O que é Normalização?**
- Processo de organização dos dados
- Elimina redundâncias
- Previne anomalias de inserção, atualização e exclusão

**Formas Normais Principais:**
- **1FN**: Atomicidade dos dados
- **2FN**: Dependência total da chave primária
- **3FN**: Elimina dependências transitivas

---

## Slide 14: **SQL - Da Modelagem à Implementação**
**Exemplo de criação de tabelas:**
```sql
CREATE TABLE Cliente (
    CPF VARCHAR(11) PRIMARY KEY,
    Nome VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE,
    DataCadastro DATE DEFAULT CURRENT_DATE
);

CREATE TABLE Pedido (
    Numero INT PRIMARY KEY AUTO_INCREMENT,
    CPF_Cliente VARCHAR(11),
    DataPedido DATE,
    ValorTotal DECIMAL(10,2),
    FOREIGN KEY (CPF_Cliente) REFERENCES Cliente(CPF)
);
```

---

## Slide 15: **Boas Práticas em Diagramação**
**Dicas para bons diagramas:**
- Use nomes claros e consistentes
- Mantenha o diagrama organizado
- Documente decisões importantes
- Revise com a equipe
- Atualize conforme mudanças

**Erros Comuns:**
- Sobrecarregar o diagrama
- Ignorar cardinalidades
- Esquecer atributos importantes
- Não validar com stakeholders

---

## Slide 16: **Caso Prático Completo**
**Sistema de Biblioteca Digital:**
1. **Requisitos identificados**:
   - Cadastro de usuários e livros
   - Controle de empréstimos e devoluções
   - Reserva de livros
   - Multas por atraso

2. **MER resultante**:
   - Entidades: Usuário, Livro, Empréstimo, Reserva
   - Relacionamentos: Usuário → Empréstimo → Livro

---

## Slide 17: **Ferramentas e Tecnologias**
**Para Análise de Requisitos:**
- Jira, Trello
- Confluence
- Figma (prototipagem)
- Draw.io (diagramas)

**Para Modelagem de BD:**
- MySQL Workbench
- pgModeler (PostgreSQL)
- SQL Server Management Studio
- DB Designer

---

## Slide 18: **Validação e Verificação**
**Como validar o modelo?**
- Revisão com usuários finais
- Prototipagem e testes de usabilidade
- Análise de casos de uso
- Simulação de processos

**Checklist de validação:**
- [ ] Todos os requisitos estão atendidos?
- [ ] As cardinalidades estão corretas?
- [ ] As chaves primárias estão definidas?
- [ ] As relações estão otimizadas?

---

## Slide 19: **Manutenção e Evolução**
**O ciclo não para na implementação:**
- Monitoramento de performance
- Análise de novas necessidades
- Adaptação a mudanças de negócio
- Documentação de alterações

**Versionamento:**
- Controle de mudanças no modelo
- Histórico de evolução
- Backup de versões anteriores

---

## Slide 20: **Conclusão**
**Pontos Chave:**
1. **Requisitos bem definidos** são fundamentais para o sucesso
2. **Modelagem de dados** transforma requisitos em estrutura
3. **Diagramas** facilitam comunicação e entendimento
4. **Iteração constante** entre análise e modelagem

**Benefícios da Abordagem Estruturada:**
- 🎯 Maior precisão no atendimento às necessidades
- ⏱️ Redução de retrabalho
- 💰 Otimização de custos
- ✅ Melhor qualidade do produto final

---

## Slide 21: **Perguntas?**
**Obrigado!**

**Contato:**
[Seus dados de contato]

**Próximos passos:**
- Workshop prático de modelagem
- Deep dive em SQL avançado
- Estudo de casos reais

---

**Material Complementar Sugerido:**
- Livro: "Análise Essencial" de Steve McMenamin
- Documentação: MySQL Reference Manual
- Ferramenta: Draw.io para prática de diagramas
- Curso: Modelagem de Dados na Udemy/Coursera
