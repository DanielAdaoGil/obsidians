# PROMPT DE ESPECIFICAÇÃO TÉCNICA E FUNCIONAL
## Sistema de Gestão de Membros — Clube de Embaixadores Cruzeiro do Sul

**Instituição:** Igreja Adventista do Sétimo Dia
**Missão:** Missão Sul de Luanda & Cabinda
**Ministério Jovem:** Vila Estoril
**Clube:** Clube de Embaixadores Cruzeiro do Sul

---

## PAPEL E POSTURA DA EQUIPA

Atue como uma equipa sénior multidisciplinar composta por:

- **Arquiteto de Software** — responsável pela estrutura técnica, padrões de projeto e preparação para escalabilidade futura.
- **Engenheiro Full Stack** — responsável pela implementação de frontend e backend.
- **Especialista em UX/UI** — responsável pela identidade visual, usabilidade e experiência do utilizador.
- **Especialista em Segurança Web (AppSec)** — responsável por garantir conformidade com boas práticas de segurança (OWASP Top 10, OWASP ASVS).
- **Especialista em Sistemas de Gestão Institucional** — responsável pelas regras de negócio do Clube.
- **Especialista em Bases de Dados** — responsável pela modelagem relacional, integridade e performance.
- **Especialista em Geração de Documentos PDF** — responsável pela fidelidade dos documentos gerados face aos modelos oficiais.
- **QA / Test Engineer** — responsável pela cobertura de testes e validação de regras críticas.

Cada decisão de arquitetura, design e implementação deve ser tomada considerando estas sete perspetivas em conjunto, priorizando sempre segurança e integridade dos dados sobre estética.

---

## OBJETIVO GERAL

Projetar e desenvolver um **sistema web profissional, institucional e seguro** cujo propósito é a **descentralização, centralização e organização digital da informação do Clube**, permitindo que utilizadores autorizados possam **cadastrar, consultar, gerir, filtrar e gerar documentos** relacionados aos membros do Clube de Embaixadores Cruzeiro do Sul.

### Escopo da primeira fase (obrigatório)

1. Cadastro de Membros
2. Gestão de Membros
3. Consulta de Membros
4. Visualização detalhada do membro
5. Geração da Ficha Individual do Membro em PDF
6. Geração de Lista de Membros (com exportação em PDF)
7. Filtros e ordenação de membros

### Fora do escopo desta fase (mas a arquitetura deve prever)

- Gestão financeira e relatórios financeiros
- Fichas de inscrição
- Gestão de atividades e eventos
- Gestão de classes/categorias avançadas
- Gestão de liderança avançada
- Estatísticas avançadas
- Outros módulos administrativos futuros

> A arquitetura (base de dados, autenticação, autorização, camada de serviços) deve ser desenhada desde já para acomodar estes módulos sem necessidade de reengenharia estrutural.

---

## 🔒 REGRA ABSOLUTA DE IDENTIDADE VISUAL (NÃO NEGOCIÁVEL)

> **Não substituir, alterar, aproximar ou inventar a paleta de cores institucional.**
> Todos os componentes da aplicação — botões, cards, sidebar, navbar, tabelas, badges, gráficos, estados, ícones, formulários, modais e documentos gerados — devem utilizar **exclusivamente** as variáveis de cor institucionais definidas na secção 1 (Identidade Visual), tanto em Light Mode como em Dark Mode.
>
> - O **azul profundo/royal** é a cor estrutural dominante da aplicação.
> - O **dourado/amarelo** é a cor de destaque (ações principais, indicadores, estados selecionados e elementos institucionais) — nunca a cor dominante.
> - Nenhuma paleta genérica de dashboard (verde, roxo, laranja, tons neutros de frameworks padrão, etc.) pode substituir estas cores em qualquer componente, biblioteca de UI ou tema de terceiros utilizado.
> - Esta regra aplica-se igualmente à Ficha Individual em PDF e à Lista de Membros em PDF: os documentos devem refletir a mesma identidade visual (azul/dourado) usada no modelo oficial e no logótipo do Clube.
> - Qualquer biblioteca, template ou componente de terceiros adotado deve ser tematizado (via variáveis CSS/design tokens) para respeitar esta paleta — nunca utilizado com as suas cores padrão.

A identidade visual deve ser diretamente inspirada no logótipo oficial fornecido (brasão azul profundo com estrelas, contorno dourado, base em tons de cinzento escuro/preto representando a montanha, e o texto "Vila Estoril").

---

## 1. IDENTIDADE VISUAL

A interface deve transmitir: **profissionalismo, organização, juventude, liderança, tecnologia, confiança, identidade institucional e elegância.**

**Paleta de cores (base no logótipo oficial):**

| Papel | Cor |
|---|---|
| Cor estrutural dominante | Azul profundo / azul royal |
| Cor estrutural secundária | Azul escuro |
| Cor de destaque (accent) | Dourado / amarelo |
| Fundo neutro claro | Branco |
| Contraste / texto escuro | Cinza escuro / preto |

O dourado deve ser reservado para: botões principais (call-to-action), ícones de destaque, indicadores de estado, linhas decorativas, elementos selecionados/ativos e elementos de identidade institucional (brasão, cabeçalhos de documentos).

**É expressamente proibido** utilizar uma aparência genérica de dashboard "de prateleira". A identidade visual deve ser exclusiva do Clube de Embaixadores Cruzeiro do Sul, refletindo o brasão fornecido.

---

## 2. LIGHT MODE E DARK MODE

- Implementar alternância Light/Dark através de um botão visível e acessível.
- A preferência deve ser **persistente** (guardada por utilizador) e aplicada globalmente a toda a aplicação, incluindo modais, tabelas e formulários.

**Light Mode:** fundo claro, cards brancos, azul institucional como estrutura, dourado como accent, texto escuro.
**Dark Mode:** fundo azul/preto muito escuro, cards em tons escuros, texto claro, azul e dourado preservados como identidade.

Garantir contraste adequado (mínimo AA do WCAG) em ambos os modos.

---

## 3. RESPONSIVIDADE

O sistema deve ser **totalmente responsivo** em desktop, laptop, tablet e smartphone, com **adaptação real** (não apenas redimensionamento) de: sidebar, navbar, cards, formulários, tabelas, filtros, botões, modais, uploads e visualização de documentos.

Em mobile, tabelas extensas devem adotar scroll horizontal controlado **ou** transformação dos registos em cards/listas responsivas (ver secção 48).

---

## 4. ESTRUTURA PRINCIPAL

**Sidebar:**

- Dashboard
- Membros
  - Cadastrar Membro
  - Consultar Membros
  - Lista de Membros
- Relatórios *(Em breve)*
- Financeiro *(Em breve)*
- Configurações

Nesta primeira fase, apenas as funcionalidades de Membros devem estar ativas. As demais devem exibir claramente o rótulo **"Em breve"**, sem simular funcionalidades inexistentes.

---

## 5. DASHBOARD INICIAL

Indicadores institucionais (calculados dinamicamente a partir da base de dados — nunca armazenados manualmente):

- Total de Membros
- Membros Masculinos / Femininos
- Membros Batizados / Não Batizados
- Líderes
- J.A.
- Outros

**Atividade recente:** últimos membros cadastrados, últimas alterações, últimos documentos gerados.

**Atalhos rápidos:** `+ Cadastrar Membro` · `Consultar Membros` · `Gerar Lista`

---

## 6. MÓDULO — CADASTRO DE MEMBROS

Formulário profissional organizado por secções — **nunca** um formulário único e extenso sem estrutura. Utilizar preferencialmente um **Wizard com indicador de progresso**:

`01` Dados Pessoais → `02` Dados Eclesiásticos → `03` Dados do Clube → `04` Contactos de Emergência → `05` Informação de Saúde → `06` Documentos e Fotografia → `07` Compromisso e Confirmação

---

## 7. DADOS PESSOAIS

Campos (baseados na ficha oficial):

- Nome completo * · Alcunha · Sexo * (Masculino/Feminino) · Nome do Pai · Nome da Mãe
- Data de nascimento * · **Idade (calculada automaticamente, nunca inserida manualmente)**
- Nº do Bilhete de Identidade/BI * · Naturalidade · Província · Endereço · Bairro
- Escolaridade · Telefone/Telemóvel * · E-mail

**Regra de cálculo:** a idade é derivada da data de nascimento e recalculada dinamicamente (ex.: nascimento em 15/08/2000 → idade atual apresentada automaticamente). O sistema deve impedir datas de nascimento impossíveis (futuras ou incompatíveis com a idade mínima do Clube).

**Alcunha (opcional):** "Nome pelo qual o membro é conhecido por amigos e pessoas próximas."

---

## 8. DOCUMENTO DE IDENTIFICAÇÃO (BI)

- Anexo obrigatório no cadastro. Formatos aceites: **PDF, JPG, JPEG, PNG, WEBP**. Tamanho máximo: **1 MB**.
- Validação de tamanho e tipo **no frontend E no backend** (nunca confiar apenas na validação do navegador), incluindo validação real de MIME type, extensão e conteúdo do ficheiro.
- Armazenamento fora de diretórios publicamente acessíveis; acesso sujeito a autenticação e autorização.
- Nome físico do ficheiro nunca corresponde ao nome original enviado — gerar identificador interno seguro (UUID).

---

## 9. FOTOGRAFIA DO MEMBRO

- Solicitada no cadastro, com uniforme de Classe A/gala, para uso na ficha individual em PDF.
- Formatos: JPG, JPEG, PNG, WEBP. Tamanho máximo: 1 MB.
- Preview obrigatório antes do envio, com opção de substituição antes de concluir o cadastro.
- Armazenamento seguro, seguindo as mesmas regras da secção 8.

---

## 10. DADOS ECLESIÁSTICOS

- Igreja · Distrito · Região · Batizado? (Sim/Não)
- Se **Sim**: exibir Igreja onde foi batizado e **Data de Batismo** (necessária para calcular "Anos de Batismo").
- Se **Não**: os campos relacionados ao batismo ficam desativados e não obrigatórios.

---

## 11. DADOS DO CLUBE

- Data de entrada/investidura no Clube · Clube anterior (se aplicável) · Data de investidura
- Medalha de Dedicação: Nenhuma / Prata / Ouro
- Categoria: J.A. / Líder / Líder Master / Líder Master Avançado

**"Anos no Clube" são sempre calculados automaticamente** a partir da data de entrada/investidura — nunca inseridos manualmente.

---

## 12. DIREÇÃO DO CLUBE

- Campo obrigatório: **"Pertence à Direção?"** (Sim/Não)
- Se **Sim**: exibir obrigatoriamente **"Cargo que ocupa"** (Diretor, Diretor Associado, Secretário, Tesoureiro, Capelão, Conselheiro, Outro).
- O campo "Cargo" só é obrigatório quando Pertence à Direção = Sim.

---

## 13. CONTACTOS DE EMERGÊNCIA

Secção com pelo menos dois contactos, estruturada conforme o documento oficial:

- **Contacto 1:** Nome/Familiar · Telefone
- **Contacto 2:** Nome/Familiar · Telefone

---

## 14. INFORMAÇÃO DE SAÚDE (dados sensíveis)

- Grupo sanguíneo · Vacina contra o Tétano (Sim/Não) · Sofre de · Medicação

Aplicar **proteção reforçada**: apenas utilizadores autorizados podem visualizar estes dados; nunca expor informação médica em tabelas gerais ou listagens.

---

## 15. DOCUMENTOS DO MEMBRO

Área específica para: fotocópia do BI e fotografia oficial. Visualização/substituição restrita a utilizadores autorizados. Nunca disponibilizar ficheiros via URLs públicas — controlo de acesso obrigatório no servidor.

---

## 16. COMPROMISSO PESSOAL

Ao final do cadastro, apresentar (sem alterar o conteúdo oficial da declaração):

- [ ] Li e compreendi o compromisso pessoal.
- [ ] Confirmo que as informações fornecidas são verdadeiras.
- [ ] Aceito realizar o trabalho de forma voluntária.

Incluir campo de **Assinatura/Confirmação**, implementado de forma juridicamente e administrativamente adequada.

---

## 17. VALIDAÇÃO DO FORMULÁRIO

Validação em frontend e backend, com campos obrigatórios claramente identificados e mensagens de erro específicas (ex.: "Nome completo é obrigatório.", "Ficheiro superior a 1 MB.", "Data de nascimento inválida."). Dados já preenchidos nunca devem ser apagados em caso de erro.

---

## 18. Nº ÚNICO DO MEMBRO

Cada membro possui um ID interno **e** um código legível gerado automaticamente, sem possibilidade de duplicação. Formato: `CES-2026-0001`, `CES-2026-0002`, etc.

---

## 19. VERIFICAÇÃO DE DUPLICIDADE

Antes de criar um membro, verificar duplicados por BI, Telemóvel e E-mail (quando informado). O BI deve ser único. Em caso de duplicidade, exibir alerta ("Já existe um membro cadastrado com este Nº de BI.") e impedir a criação de um segundo registo.

---

## 20. CONSULTAR MEMBROS

Página de pesquisa inteligente por Nome, Nº BI, Nº Telemóvel ou Alcunha, com suporte a pesquisa parcial (ex.: "João" retorna todos os "João" cadastrados).

Resultados em **tabela** (desktop) e **cards** (mobile), com colunas: Fotografia, Nº Membro, Nome, Alcunha, Sexo, Idade, Telefone, Categoria, Batizado, Estado, e ação "Ver detalhes".

---

## 21. PÁGINA DE DETALHES DO MEMBRO

Cabeçalho com fotografia, nome, nº do membro, categoria, idade e estado, seguido pelas secções: Dados Pessoais, Dados Eclesiásticos, Dados do Clube, Direção, Contactos de Emergência, Informação de Saúde, Documentos e Compromisso.

Ações: `Editar` · `Gerar Ficha PDF` · `Voltar`

---

## 22. GERAÇÃO DA FICHA INDIVIDUAL EM PDF

Botão **"Gerar Ficha PDF"**, produzindo um documento que **respeita fielmente o modelo oficial fornecido** (estrutura, títulos, campos, posicionamento, área da fotografia, assinaturas e identificação do Clube) — nunca um PDF genérico.

- Preenchimento automático dos dados do membro; fotografia colocada no espaço destinado no modelo.
- Manter a declaração/compromisso oficial do modelo, sem alterações de conteúdo.
- Resultado pronto para impressão.
- Nome do ficheiro: `Ficha_Membro_NOME_CES-2026-0001.pdf`

---

## 23. GERAR LISTA DE MEMBROS

Página iniciada com 3 cards de resumo, calculados dinamicamente a partir da base de dados:

1. **Total de Membros**
2. **Total de Membros Masculinos**
3. **Total de Membros Femininos**

---

## 24–29. FILTROS DISPONÍVEIS

| Filtro | Critério |
|---|---|
| **Idade** | Campo numérico + operador (`>`, `>=`, `<`, `<=`, `=`) |
| **Mês** | Mês da data de nascimento (Janeiro a Dezembro) |
| **Batismo** | Todos / Batizado / Não Batizado |
| **Anos no Clube** | Campo numérico + operador, calculado a partir da data de investidura |
| **Anos de Batismo** | Campo numérico + operador, calculado a partir da data de batismo (apenas membros batizados) |
| **Transferência** | Idade > 22 **E** categoria ≠ J.A. **E** categoria ≠ Líder **E** não pertence à Direção — regra aplicada obrigatoriamente no backend, nunca apenas ocultada no frontend. Exibir indicação "Elegível para transferência" |

Todos os valores calculados (idade, anos no clube, anos de batismo) são sempre derivados dinamicamente das respetivas datas — nunca armazenados ou inseridos manualmente.

---

## 30. ORDENAÇÃO

- **Por Idade:** Crescente / Decrescente
- **Alfabética (nome completo):** A → Z / Z → A

---

## 31. RESULTADOS DA LISTA

Após aplicação de filtros, exibir "Total encontrado: XX membros" e tabela com: Nº, Fotografia, Nº Membro, Nome, Alcunha, Sexo, Idade, Telefone, Categoria, Batismo, Anos no Clube, Anos de Batismo. Cada linha é clicável, abrindo os detalhes do membro. Ações: `Limpar filtros` · `Aplicar filtros`

---

## 32. EXPORTAÇÃO E GERAÇÃO DE LISTA EM PDF *(requisito detalhado)*

A arquitetura deve estar preparada para, no futuro, suportar exportação em Excel e impressão direta. **Nesta primeira fase, é obrigatório implementar a exportação da lista em PDF**, disponível através de um botão de **"Baixar PDF"** na própria página de Lista de Membros, respeitando **exatamente os filtros e a ordenação atualmente aplicados** na consulta.

O PDF gerado deve conter:

**a) Cabeçalho institucional (obrigatório)**, contendo:
- Identidade visual do Clube (logótipo/brasão, azul e dourado conforme identidade institucional).
- Título claro identificando o tipo de documento — ex.: **"Lista de Membros"**.
- Um **resumo descritivo dos critérios aplicados**, informando ao leitor exatamente o que a lista representa. Exemplo: *"Lista de Membros — Sexo: Masculino · Batismo: Batizado · Idade ≥ 22 anos · Ordenado por: Nome (A → Z)"*. Caso nenhum filtro tenha sido aplicado, indicar *"Lista completa de membros"*.
- Data e hora de geração do documento.
- Total de registos apresentados na lista.
- Identificação de quem gerou o documento (utilizador autenticado), para fins de auditoria.

**b) Corpo do documento — tabela com os campos solicitados:**
Nº · Fotografia (miniatura, quando aplicável ao layout) · Nº do Membro · Nome · Alcunha · Sexo · Idade · Telefone · Categoria · Estado de Batismo · Anos no Clube · Anos de Batismo.

**c) Rodapé:**
Numeração de páginas e identificação institucional (Clube de Embaixadores Cruzeiro do Sul — Ministério Jovem, Vila Estoril).

**d) Requisitos técnicos:**
- Layout otimizado para impressão em A4, com tabela paginada corretamente quando o número de membros exceder uma página.
- Documento gerado no servidor, aplicando exatamente a mesma query/regra de filtragem usada na tela — nunca gerado a partir de dados manipulados apenas no frontend.
- Nome do ficheiro sugerido: `Lista_Membros_[Filtro-resumido]_[DataDeGeracao].pdf`

---

## 33. SEGURANÇA

Segurança é requisito **fundamental**, seguindo referências como OWASP Top 10, OWASP ASVS e Secure Coding Practices.

**Autenticação:** login seguro, passwords com hashing forte, sessões seguras, logout, proteção contra session fixation.

**Autorização (RBAC):**

| Perfil | Permissões |
|---|---|
| ADMIN | Acesso total |
| SECRETARIA | Cadastrar, consultar, editar, gerar documentos |
| DIREÇÃO | Consultar, visualizar informações autorizadas, gerar relatórios |
| CONSULTA | Apenas visualizar informações permitidas |

Nunca permitir acesso indevido por manipulação direta de URL (IDOR).

---

## 34. PROTEÇÃO DE DADOS

Dados armazenados (BI, telefone, endereço, fotografia, informação de saúde, dados familiares) devem ser tratados como **informação sensível/confidencial**, com HTTPS, proteção CSRF/XSS/SQL Injection, rate limiting, secure headers, validação de input, escaping de output, controlo de sessão e acesso, logs de segurança e auditoria. Passwords nunca em texto simples; documentos pessoais nunca em diretórios públicos.

---

## 35. UPLOADS SEGUROS

Limite de 1 MB; validação de MIME type real, extensão e conteúdo; renomeação de ficheiros; impedimento de execução de scripts; armazenamento fora do diretório público quando possível; autorização obrigatória para download.

**Permitido:** PDF, JPG, JPEG, PNG, WEBP.
**Rejeitado:** PHP, JS, HTML, SVG não sanitizado, EXE, ZIP e afins.

---

## 36. AUDITORIA

Registar (Audit Log): criação e alteração de membros (quem, quando, o quê), geração de PDF, consulta de documentos sensíveis, login/logout e tentativas de acesso não autorizado.

---

## 37. BASE DE DADOS

Base de dados normalizada, com entidades principais: `users`, `roles`, `members`, `emergency_contacts`, `member_documents`, `member_photos`, `audit_logs`, e estruturas auxiliares (`churches`, `districts`, `regions`, `categories`, `leadership_positions`).

Aplicar Primary Keys, Foreign Keys, Unique Constraints e Índices — especialmente em BI, Nome, Telefone, Alcunha, Data de nascimento, Categoria e Estado de batismo.

---

## 38. EXPERIÊNCIA DO UTILIZADOR

Interface moderna e limpa: cards elegantes, ícones consistentes, breadcrumbs, toast notifications, modais de confirmação, skeleton loading, empty/loading/error states, com mensagens claras (ex.: "✓ Membro cadastrado com sucesso.").

---

## 39. CONFIRMAÇÕES

Ações críticas (excluir membro, alterar documento, substituir fotografia) exigem confirmação explícita. Preferir **soft delete** para membros.

---

## 40. PERFORMANCE

Preparado para centenas ou milhares de membros: paginação, pesquisa e filtros server-side, índices de base de dados, lazy loading quando necessário. Nunca carregar todos os membros de uma vez.

---

## 41. ACESSIBILIDADE (WCAG)

Contraste adequado, navegação por teclado, labels nos campos, mensagens de erro acessíveis, estados de foco visíveis, botões identificáveis e independência de cor como único indicador.

---

## 42. ARQUITETURA

Código limpo e modular, com separação clara entre UI, lógica de negócio, validação, persistência, serviços, geração de PDF, uploads, autenticação e autorização. Utilizar Services, Repositories, Form Requests/Validators, Policies/Permissions, DTOs e componentes reutilizáveis conforme aplicável.

---

## 43. API / BACKEND

Endpoints RESTful, com autenticação e autorização em todos os endpoints protegidos:

```
GET    /members
POST   /members
GET    /members/{id}
PUT    /members/{id}
DELETE /members/{id}
GET    /members/search
GET    /members/{id}/pdf
GET    /members/list
GET    /members/list/pdf
```

---

## 44. ESTADOS DO MEMBRO

Campo `status`: Ativo / Inativo / Transferido / Falecido / Suspenso. Preservar histórico — evitar exclusão física desnecessária.

---

## 45. DASHBOARD E ESTATÍSTICAS

Todos os indicadores calculados diretamente da base de dados via consultas agregadas (`COUNT`, filtros), nunca armazenados manualmente.

---

## 46. DESIGN DOS FORMULÁRIOS

Cada campo deve ter: label, campo de input, descrição (quando necessário), validação e mensagem de erro clara.

---

## 47. PREVIEW DA FICHA

Opção **"Visualizar Ficha"** para prévia fiel do documento antes de `Baixar PDF`.

---

## 48. RESPONSIVIDADE DA TABELA

**Desktop:** tabela completa. **Mobile:** cada membro transformado em card (foto, nome, nº do membro, idade, sexo, categoria, estado de batismo, botão "Ver detalhes").

---

## 49. MICROINTERAÇÕES

Hover, transições, loading, feedback visual e animações suaves — discretas, sem comprometer o caráter institucional e profissional do sistema.

---

## 50. REQUISITO CRÍTICO — MODELO PDF OFICIAL

O documento PDF fornecido é a **fonte visual e estrutural oficial** da ficha. Não inventar campos além dos explicitamente solicitados:

- Alcunha
- Idade calculada automaticamente
- Data de batismo
- Pertence à Direção? / Cargo da Direção
- Upload do BI
- Fotografia com uniforme de Classe A/Gala

Preservar a terminologia oficial: *"Igreja Adventista do Sétimo Dia"*, *"Missão Sul de Luanda & Cabinda"*, *"Ministério Jovem – Vila Estoril"*, *"Clube de Embaixadores Cruzeiro do Sul"*.

---

## 51. ESCOPO DA PRIMEIRA FASE — EXCLUSÕES EXPLÍCITAS

Não desenvolver agora: gestão financeira completa, contabilidade, pagamentos, caixa, receitas/despesas, gestão de eventos e atividades, gestão de medalhas completa, gestão de presença, mensagens e notificações avançadas. A arquitetura deve estar preparada para acomodar estes módulos futuramente.

---

## 52. QUALIDADE DO CÓDIGO

Código limpo, modular, escalável, seguro, documentado e manutenível. Evitar: duplicação, variáveis genéricas, queries inseguras, dados sensíveis expostos no frontend, credenciais hardcoded, secrets no Git, código morto e dependências desnecessárias. Utilizar variáveis de ambiente.

---

## 53. TESTES

Cobertura obrigatória para: cadastro, validação, login, permissões, pesquisa, filtros, ordenação, cálculo de idade/anos no clube/anos de batismo, regra de transferência, upload (incluindo limite de 1 MB e formato inválido), geração de PDF (ficha individual e lista), BI/telefone duplicado, membro não batizado, membro na Direção e fora dela, e dados incompletos.

---

## 54. REGRAS DE CÁLCULO

```
idade         = hoje − data_de_nascimento
anos_clube    = hoje − data_de_entrada_investidura
anos_batismo  = hoje − data_de_batismo
```

Nunca permitir inserção manual destes valores.

---

## 55. REGRA DE TRANSFERÊNCIA

```
elegível_transferência =
    idade > 22
    AND categoria != "J.A."
    AND categoria != "Líder"
    AND pertence_direcao = false
```

Regra centralizada e aplicada no backend.

---

## 56. SEGURANÇA DE ACESSO A DOCUMENTOS

Ao aceder a "Ver BI" ou "Baixar BI", validar: (1) utilizador autenticado, (2) permissão adequada, (3) documento pertence ao membro solicitado, (4) pedido válido. Nunca confiar apenas no ID enviado pelo frontend — prevenir IDOR/BOLA.

---

## 57. INTERFACE FINAL

O sistema deve transmitir, à primeira vista: *"Este é um sistema oficial de gestão do Clube de Embaixadores Cruzeiro do Sul."* Evitar aparência de template genérico — usar consistentemente a identidade visual do logótipo.

---

## 58. CHECKLIST DE ENTREGA

1. Arquitetura · 2. Base de dados · 3. Autenticação · 4. Autorização · 5. Módulo de membros · 6. Formulário de cadastro · 7. Uploads · 8. Consulta · 9. Detalhes · 10. Filtros · 11. Ordenação · 12. Cálculos automáticos · 13. Geração de PDF (ficha e lista) · 14. Light/Dark Mode · 15. Responsividade · 16. Segurança · 17. Testes · 18. Revisão de código · 19. Revisão de segurança · 20. Testes de responsividade

O projeto não deve ser considerado concluído apenas por estar visualmente pronto.

---

## 59. NÃO INVENTAR REQUISITOS

Quando uma informação não estiver definida, não inventar regras de negócio nem campos desnecessários, nem alterar o significado dos campos da ficha oficial. Utilizar a documentação fornecida como fonte principal. Quando for estritamente necessário adicionar algo para viabilizar uma funcionalidade solicitada, implementar apenas o mínimo indispensável (ex.: "Data de Batismo" é necessária para calcular "Anos de Batismo", mesmo não constando no PDF original).

---

## 60. RESULTADO ESPERADO

Sistema web institucional, seguro, moderno, responsivo e escalável para o **Clube de Embaixadores Cruzeiro do Sul**, permitindo à Secretaria/Direção:

✓ Cadastrar, consultar, editar e pesquisar membros (por Nome, BI, Telefone ou Alcunha)
✓ Guardar com segurança BI e fotografia oficial
✓ Visualizar detalhes completos do membro
✓ Calcular automaticamente idade, anos no Clube e anos de batismo
✓ Filtrar e ordenar membros, identificando elegíveis para transferência
✓ Gerar a Ficha Individual em PDF fiel ao modelo oficial, com fotografia
✓ Gerar a Lista de Membros com download em PDF, contendo cabeçalho explicativo (o que a lista representa e quais filtros foram aplicados) e tabela com todos os campos solicitados
✓ Operar em Light/Dark Mode, com identidade visual azul e dourada preservada em toda a aplicação
✓ Funcionar corretamente em desktop, tablet e smartphone
✓ Proteger dados pessoais e documentos sensíveis
✓ Registar ações relevantes através de auditoria

### Ordem de prioridade

1. Segurança
2. Integridade dos dados
3. Funcionalidade
4. Usabilidade
5. Responsividade
6. Performance
7. Design
8. Escalabilidade

**Segurança e integridade dos dados nunca devem ser sacrificadas em favor da aparência visual.**