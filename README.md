# cofre-indice

Skill para Claude Code que organiza a memória de um projeto como um cofre no estilo Obsidian, guiado por um **índice mestre**.

Em vez de ler vários documentos ou fazer buscas que nem sempre caem no lugar certo, o agente lê primeiro um índice curto que diz onde está cada assunto e abre só a nota que interessa. Assim gasta menos tokens e erra menos.

## Como funciona

### 1. O cofre (`knowledge-local/`)
É uma pasta de Markdown comum dentro do projeto. Não precisa do Obsidian: ele é opcional, só pra quem quiser navegar pelos links e pelo grafo.

```
knowledge-local/
  00-inicio.md            ← índice mestre
  01-visao.md
  02-estado.md
  02-arquitetura/mapa-do-codigo.md
  03-regras/...
  04-operacao/validacao.md
```

Cada nota trata de um assunto só e começa com um cabeçalho com `title`, `updated`, `status`, `tags` e `sources`.

### 2. O índice mestre (`00-inicio.md`)
É o sumário do cofre, escrito como uma tabela **"Preciso de… → Próxima nota"**. A primeira coluna é a pergunta como alguém a faria, e é isso que permite ao agente decidir sem abrir arquivo nenhum.

| Preciso de… | Próxima nota |
| --- | --- |
| Retomar o trabalho e saber o que foi concluído | Estado atual |
| Entender o produto e os fluxos | Visão |
| Localizar componentes, APIs e bibliotecas | Mapa do código |
| Comandos, testes e limites de evidência | Validação |

### 3. As duas regras da skill
1. **Índice primeiro:** o agente sempre lê o índice e abre de 1 a 3 notas, nunca o acervo inteiro.
2. **Mudou nota, muda o índice:** toda criação ou alteração de nota atualiza o índice na mesma tarefa. Decisões, regras e o estado do trabalho são registrados sem esperar pedido.

## Conteúdo

- `cofre-indice/SKILL.md`: a skill.
- `cofre-indice/modelos/CLAUDE-trecho.md`: trecho para colar no `CLAUDE.md` do projeto.

## Instalação (Claude Code)

1. Copie a pasta `cofre-indice` para `~/.claude/skills/` para usar em todos os projetos, ou para `.claude/skills/` dentro de um repositório para compartilhar com quem clonar.
2. Cole o conteúdo de `modelos/CLAUDE-trecho.md` no `CLAUDE.md` do projeto. Isso garante que o índice seja lido mesmo quando a skill não for acionada sozinha.
3. Na primeira tarefa, peça ao agente para criar o cofre. Ele monta `00-inicio.md`, `01-visao.md` e `02-estado.md` e cria as outras notas conforme o trabalho avança.

## Versionar ou não o cofre

- **Projeto individual:** deixe `knowledge-local/` fora do Git, por exemplo em `.git/info/exclude`.
- **Conhecimento de equipe:** versione o cofre num repositório compartilhado, para todos lerem e atualizarem o mesmo índice. Informação restrita deve ficar em outro cofre, com acesso controlado.

## Cuidados

- Não guarde no cofre senhas, tokens, chaves, dados pessoais (LGPD) nem transcrições inteiras.
- Índice desatualizado é pior que índice nenhum. É por isso que a regra 2 existe.
