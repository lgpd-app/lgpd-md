<p align="center">
  <img src="./lgpd-md.svg" alt="lgpd.md" width="200">
</p>

# lgpd.md

Um padrão aberto para declarar conformidade LGPD em websites.

Um arquivo YAML na raiz do site — legível por humanos, crawlers e ferramentas de auditoria. Sem dependências, sem vendor lock-in.

## O que é

O `lgpd.md` é um arquivo padronizado que declara como um site trata dados pessoais sob a [Lei 13.709/2018 (LGPD)](http://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/L13709compilado.htm). Funciona como o `robots.txt` funciona para crawlers ou o `security.txt` funciona para pesquisadores de segurança — mas para privacidade.

O arquivo combina:
- **Frontmatter YAML** — dados estruturados, validáveis por JSON Schema
- **Corpo Markdown** — contexto em prosa, legível por humanos e LLMs

## Por que usar

Sites brasileiros precisam informar como tratam dados pessoais. Na prática, essa informação está dispersa em políticas de privacidade extensas, banners de cookies e páginas jurídicas — todas escritas para humanos, nenhuma para máquinas.

O `lgpd.md` resolve isso com um formato padronizado que:
- Ferramentas de auditoria podem parsear automaticamente
- DPOs podem verificar em segundos
- Crawlers de compliance podem indexar em escala
- LLMs podem interpretar sem ambiguidade

## Quick Start

**1. Crie o arquivo** na raiz do seu site:

```yaml
---
spec: "1.0"
atualizado: 2026-05-31
expira: 2027-05-31
status: conforme

controlador:
  nome: "Sua Empresa Ltda"
  cnpj: "12.345.678/0001-90"
  contato: "privacidade@suaempresa.com.br"

encarregado:
  nome: "Nome do DPO"
  contato: "dpo@suaempresa.com.br"

direitos:
  canal: "https://suaempresa.com.br/privacidade/direitos"
  prazo: 15

politica:
  url: "https://suaempresa.com.br/privacidade"

bases_legais:
  - finalidade: "Prestação do serviço"
    base: "execução de contrato"
    dados: ["nome", "email"]
---

# lgpd.md

> Declaração de conformidade LGPD da Sua Empresa Ltda.
```

**2. Valide** contra o JSON Schema:

```bash
# Com ajv (Node.js)
npx ajv validate -s https://lgpd.md/schema.json -d ./lgpd.md

# Com yq + ajv
yq -o=json '.frontmatter' lgpd.md | npx ajv validate -s schema.json
```

**3. Faça deploy** — o arquivo deve estar acessível em `https://seusite.com.br/lgpd.md`

## Estrutura do Repositório

```
lgpd-md/
├── README.md              ← Este arquivo
├── LGPD-MD-SPEC.md        ← Especificação formal completa
├── schema.json            ← JSON Schema para validação do frontmatter
├── examples/
│   ├── blog-pessoal.md    ← Exemplo mínimo
│   ├── e-commerce.md      ← Exemplo com cookies e transferência internacional
│   └── saas-b2b.md        ← Exemplo com múltiplas bases legais
├── CONTRIBUTING.md        ← Como contribuir
└── LICENSE                ← Apache 2.0
```

## Campos Obrigatórios

| Campo | Descrição |
|-------|-----------|
| `spec` | Versão da spec (`"1.0"`) |
| `atualizado` | Data da última atualização (YYYY-MM-DD) |
| `expira` | Data de expiração — força revisão periódica |
| `status` | `conforme`, `parcial` ou `em-adequação` |
| `controlador` | Nome, CNPJ e contato do controlador |
| `encarregado` | Nome e contato do DPO |
| `direitos` | Canal e prazo para exercício de direitos (Art. 18) |
| `politica` | URL da política de privacidade |
| `bases_legais` | Mapeamento finalidade → base legal → dados |

Campos opcionais: `cookies`, `transferencia_internacional`, `scripts_terceiros`.

→ [Leia a especificação completa](./LGPD-MD-SPEC.md)

## Validação

O frontmatter YAML é validável contra o [JSON Schema](./schema.json) publicado em:

- `https://lgpd.md/schema.json`
- `https://github.com/lgpd-app/lgpd-md/blob/main/schema.json`

## Exemplos

- [Blog pessoal](./examples/blog-pessoal.md) — coleta mínima, controlador pessoa física
- [E-commerce](./examples/e-commerce.md) — cookies, pagamento, transferência internacional
- [SaaS B2B](./examples/saas-b2b.md) — múltiplas bases legais, status parcial

## Relação com Outros Padrões

| Padrão | Relação |
|--------|---------|
| `robots.txt` | Coexiste — lgpd.md não controla acesso de crawlers |
| `security.txt` | Complementar — security.txt trata vulnerabilidades; lgpd.md trata privacidade |
| `llms.txt` | Complementar — LLMs podem referenciar lgpd.md para entender práticas de dados |
| Política de privacidade | lgpd.md complementa com dados estruturados; a política é o documento legal completo |

## Skills para Agentes de IA

O ecossistema lgpd.md inclui [skills](https://github.com/lgpd-app/skills) que permitem a agentes de IA trabalhar com conformidade LGPD:

| Skill | Descrição |
|-------|-----------|
| [`lgpd-check`](https://github.com/lgpd-app/skills/tree/main/skills/lgpd-check) | Audita websites para conformidade LGPD — verifica política de privacidade, cookies, minimização de dados, transferência internacional, direitos do titular e scripts de terceiros |
| [`lgpd-md`](https://github.com/lgpd-app/skills/tree/main/skills/lgpd-md) | Gera e valida arquivos lgpd.md a partir da política de privacidade e documentos existentes do site |

Instale com:

```bash
npx skills add lgpd-app/skills --skill "LGPD Check"
npx skills add lgpd-app/skills --skill lgpd-md
```

## Links

- **Site**: [lgpd.md](https://lgpd.md)
- **Auditoria automatizada**: [lgpd.app](https://lgpd.app)
- **Spec formal**: [LGPD-MD-SPEC.md](./LGPD-MD-SPEC.md)
- **JSON Schema**: [schema.json](./schema.json)

## Autor

**Fabricio Telles** — Gerente de Tecnologia — [ft.ia.br](https://ft.ia.br/)

## Contribuindo

Contribuições são bem-vindas. Veja [CONTRIBUTING.md](./CONTRIBUTING.md) para detalhes.

## Licença

[Apache 2.0](./LICENSE)

## Disclaimer

Esta proposta de padrão e suas ferramentas propostas não substituem a assessoria de um advogado especialista. É um mecanismo para facilitar a descoberta de informações de privacidade em sites brasileiros. O usuário é o único responsável pelas informações fornecidas por ele mesmo em seu site na web.