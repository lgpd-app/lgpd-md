# Contribuindo com o lgpd.md

Contribuições são bem-vindas. Este documento explica como participar.

## Como contribuir

### Reportar problemas

Abra uma [issue](https://github.com/lgpd-app/lgpd-md/issues) descrevendo:
- O que está errado ou pode melhorar
- Contexto relevante (artigo da LGPD, cenário de uso)
- Sugestão de correção, se tiver

### Propor mudanças

1. Fork o repositório
2. Crie uma branch (`git checkout -b melhoria/descricao`)
3. Faça suas alterações
4. Abra um Pull Request com descrição clara da mudança

### O que aceitar

- Correções factuais (referências a artigos da LGPD, resoluções da ANPD)
- Novos exemplos de arquivos lgpd.md para cenários não cobertos
- Melhorias na clareza da spec
- Traduções (a spec é em PT-BR; traduções para outros idiomas são bem-vindas)
- Ajustes no JSON Schema

### O que não aceitar

- Mudanças que quebrem compatibilidade com a versão 1.0 sem discussão prévia
- Adição de campos obrigatórios sem justificativa legal
- Conteúdo que não esteja alinhado com a Lei 13.709/2018

## Versionamento

A spec segue versionamento semântico simplificado:
- **MAJOR** (ex: 1.0 → 2.0): mudanças incompatíveis
- **MINOR** (ex: 1.0 → 1.1): novos campos opcionais, esclarecimentos

Mudanças MAJOR requerem discussão em issue antes de implementação.

## Código de conduta

Seja respeitoso. Contribuições técnicas e construtivas. Sem spam, sem autopromoção.

## Licença

Ao contribuir, você concorda que suas contribuições serão licenciadas sob [Apache 2.0](./LICENSE).
