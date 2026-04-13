# 🧠 obsidian-llm

> Transforme seu cofre do Obsidian em uma base de conhecimento gerenciada por agentes de IA — direto do terminal.

---

## O que é isso?

**obsidian-llm** é um conjunto de prompts de agente projetados para rodar em qualquer ferramenta de IA agentica via CLI (como [Qwen Code](https://github.com/QwenLM/qwen-code), Claude Code, Cursor, Windsurf, entre outros).

A ideia é simples: em vez de organizar seu cofre manualmente, você delega esse trabalho para agentes especializados. Cada agente tem uma responsabilidade única — migrar, processar, consultar ou arquivar — e eles se passam o bastão em sequência.

---

## Como funciona

O sistema usa 3 pastas como "esteiras de trabalho":

```
conteudo-bruto/     ← você joga suas notas novas aqui
cofre-obsidian/     ← o agente organiza tudo aqui
resultados/         ← respostas valiosas são salvas aqui
```

E 4 agentes que operam nessas pastas:

| Agente | Quando usar | O que faz |
|---|---|---|
| `migration-agent` | Uma vez, no setup inicial | Analisa o cofre antigo, cria a arquitetura de pastas, reescreve e migra tudo |
| `processing-agent` | Sempre que novas notas chegam | Refina, categoriza e integra novas notas ao cofre |
| `query-agent` | Para consultar o cofre | Responde perguntas em linguagem natural com base no seu conhecimento salvo |
| `results-agent` | Para salvar respostas importantes | Arquiva as melhores respostas do `query-agent` como notas permanentes |

---

## Pré-requisitos

- Uma ferramenta de IA agentica com acesso ao filesystem via CLI
  - Recomendado: **[Qwen Code](https://github.com/QwenLM/qwen-code)** (gratuito)
  - Alternativas: Claude Code, Cursor Agent, Windsurf
- Um cofre do Obsidian (ou qualquer pasta com arquivos `.md`)
- Git (para clonar o repositório)

---

## Instalação e uso

### 1. Clone o repositório

```bash
git clone https://github.com/Patrick-Barbosa/obsidian-llm.git
cd obsidian-llm
```

### 2. Configure sua estrutura de pastas

Crie as pastas de trabalho dentro do repositório (ou aponte para as existentes no seu cofre):

```bash
mkdir conteudo-bruto cofre-obsidian resultados
```

### 3. Abra seu agente de CLI

Inicie a ferramenta agentica dentro da pasta do projeto. Exemplo com Qwen Code:

```bash
qwen-code .
```

### 4. Carregue o agente certo para cada tarefa

Cada arquivo `.md` na raiz do repositório é um **prompt de sistema** para um agente específico. Carregue o conteúdo do arquivo como instrução do agente antes de começar.

---

## Fluxo recomendado

```
1ª vez:
  conteudo-bruto/ → [migration-agent] → cofre-obsidian/

Uso contínuo:
  conteudo-bruto/ → [processing-agent] → cofre-obsidian/
                                              ↓
                                        [query-agent] → resposta
                                              ↓ (se valiosa)
                                        [results-agent] → resultados/
```

---

## Filosofia do projeto

Os agentes seguem algumas regras inegociáveis:

- **Nenhum dado original pode ser perdido** durante refinamento ou migração
- **Zero alucinação** — o `query-agent` só responde com o que está no cofre
- **Separação de responsabilidades** — cada agente só age em seu domínio
- **Rastreabilidade** — todas as respostas citam a nota de origem via `[[wikilinks]]`

---

## Licença

Apache 2.0 — veja [LICENSE](./LICENSE) para detalhes.