# Publicador do site

Gatilho de publicação do site `ricardoxavier.vercel.app`. Não tem código do
site dentro: só a rotina que manda publicar.

## Por que ele existe

O site mora em `joaoxavier1974/sitejoao`, que é conta pessoal de outra pessoa.
A Vercel só enxerga repositórios da própria conta e de organizações, então
quando o repositório mudou de dono a integração que publicava sozinha a cada
commit deixou de funcionar, e não há como religá-la.

A saída óbvia seria guardar o token da Vercel dentro do repositório do site.
Esse token abre a conta inteira, incluindo as variáveis de ambiente dos outros
projetos que vivem nela, e por isso ele não foi para lá. Ficou aqui.

## Como funciona

A cada dez minutos a rotina compara duas coisas:

- o último commit de `main` no repositório do site
- o commit que está publicado na Vercel, lido do campo `commit` do deploy

Se forem iguais, ela não faz nada. Se forem diferentes, baixa o site e publica.
Também dá para disparar na mão pela aba Actions, em "Run workflow".

Quem edita o site usa o painel em `/admin` e não precisa saber de nada disso.
O efeito para quem publica é o site atualizar em alguns minutos.

## Segredos

| Nome | O que é |
|---|---|
| `VERCEL_TOKEN` | token da Vercel que autoriza publicar |
| `VERCEL_ORG_ID` | identificador da conta na Vercel |
| `VERCEL_PROJECT_ID` | identificador do projeto do site |
| `SITEJOAO_GH_TOKEN` | token do GitHub que lê o repositório do site |

Se a publicação parar de acontecer, é quase certo que um desses dois tokens foi
revogado. A aba Actions mostra qual passo falhou.
