---
name: cofre-indice
description: Base de conhecimento local em formato de cofre do Obsidian, guiada por um índice mestre (`knowledge-local/00-inicio.md`). Use SEMPRE ao começar trabalho real numa pasta de projeto ou de contexto da empresa, antes de procurar qualquer informação nela, e sempre que surgir decisão, regra de negócio, customização de cliente ou descoberta que valha guardar. Lê o índice primeiro e abre só a nota certa, em vez de varrer documentos inteiros.
---

# Cofre com índice mestre

O conhecimento fica em notas Markdown curtas, uma por assunto, dentro de `knowledge-local/`. O arquivo `knowledge-local/00-inicio.md` é o **índice mestre**: diz o que existe e quando abrir cada nota. Ler o índice custa pouco; varrer todas as notas, ou fazer buscas que caem no documento errado, custa muitos tokens.

Não precisa ter o Obsidian instalado. São arquivos `.md` comuns com links relativos; quem quiser pode abrir a pasta como cofre no Obsidian e navegar pelos links e pelo grafo.

## Regra 1 — Índice primeiro, sempre

1. Antes de qualquer coisa, leia `knowledge-local/00-inicio.md`. Ele é curto de propósito.
2. Pela tabela do índice, escolha **de uma a três notas** que respondem ao pedido e leia só elas. Siga links dessas notas apenas se precisar.
3. Busca por texto (grep) no acervo é último recurso. Se a busca achar algo que o índice deveria ter apontado, acrescente a linha no índice.
4. Não leia o acervo inteiro "para garantir". O índice é roteador, não lista de leitura.

Se `knowledge-local/` ainda não existir e o trabalho for de fato no projeto (não uma pergunta avulsa), crie a estrutura mínima da seção "Começar um cofre" e siga com o pedido.

## Regra 2 — Mudou nota, muda o índice

Ao criar, renomear, dividir, apagar ou mudar o sentido de uma nota, atualize `00-inicio.md` **na mesma tarefa**. Índice desatualizado faz o agente confiar num mapa errado.

Registre sem esperar pedido:
- decisões e o motivo delas;
- regras de negócio e customizações de cliente;
- como algo funciona, quando custou esforço descobrir;
- estado do trabalho e próximo passo, para outro chat retomar.

Não registre: diário de comandos, transcrições inteiras, senhas, tokens, chaves, dados pessoais de sócios e torcedores (LGPD), nem dados financeiros, contratuais ou estratégicos fora de cofres restritos à gestão.

## Começar um cofre

```
knowledge-local/
  00-inicio.md          ← índice mestre (sempre lido primeiro)
  01-visao.md           ← o que é o projeto/área e o objetivo
  02-estado.md          ← onde o trabalho parou, pendências, próximo passo
  <tema>/<assunto>.md   ← notas por assunto, criadas conforme surgem
```

Pastas temáticas numeradas ajudam a ordenar quando o acervo cresce, por exemplo `01-produto/`, `02-arquitetura/`, `03-regras/`, `04-operacao/`, `05-design/`, `06-trabalho/`. Crie só as que forem usadas. Nomes de arquivo em minúsculas, com hífen e descritivos: `03-regras/renovacao-plano-socio.md`, nunca `nota3.md`.

## Formato do índice

A peça-chave é a tabela **"Preciso de… → Próxima nota"**. A primeira coluna é escrita do jeito que alguém faria a pergunta; é ela que permite decidir sem abrir arquivo nenhum.

```markdown
---
title: <Projeto> - índice do conhecimento local
updated: AAAA-MM-DD
status: ativo
tags: [indice]
---

# <Projeto>: comece por aqui

Leia só o assunto que a tarefa pede. Este índice é o roteador, não uma lista de leitura.

| Preciso de… | Próxima nota |
| --- | --- |
| Retomar o trabalho e saber o que foi concluído | [Estado atual](02-estado.md) |
| Entender o produto e os fluxos | [Visão](01-visao.md) |
| Carência, multa e renovação do plano de sócio | [Renovação do plano](03-regras/renovacao-plano-socio.md) |
| Por que o PIX passa pelo gateway e não direto | [Decisão PIX](06-trabalho/decisao-pix.md) |

## Cuidados de retomada
- Instruções novas prevalecem sobre decisões antigas registradas aqui.
- O código/sistema atual comprova o que está implementado, não necessariamente a intenção final.
```

Mantenha o índice enxuto (até ~150 linhas). Se um tema crescer demais, crie um sub-índice (`03-regras/00-regras.md`) e deixe no mestre só uma linha apontando para ele.

## Formato de cada nota

```markdown
---
title: Renovação do plano de sócio
updated: AAAA-MM-DD
status: vigente | proposta | substituída | a-revalidar
tags: [regra, cliente-x]
sources: ["reunião com cliente em AAAA-MM-DD", "ticket PROJ-123"]
---

# Renovação do plano de sócio

Resumo em 1–3 linhas.

## Detalhe
...

[Índice](../00-inicio.md) · [Nota relacionada](../06-trabalho/decisao-pix.md)
```

- Uma nota, um assunto. Se começar a tratar de dois, divida e atualize o índice.
- Toda nota liga de volta ao índice e a pelo menos uma nota relacionada.
- Mudou a regra: edite a nota canônica em vez de criar "v2". Se o histórico importar, marque a antiga como `substituída` e aponte para a nova.
- Diferencie proposta, implementado, validado e histórico a revalidar no campo `status`.

## Antes de encerrar a tarefa

1. A informação nova está na nota certa?
2. O índice tem uma linha "Preciso de…" que leva até ela?
3. `02-estado.md` diz onde parou e qual o próximo passo?
