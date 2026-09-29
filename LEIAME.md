# Cátedra — organizador de estudos da magistratura

Aplicativo de página única (HTML) que distribui o seu material de estudo pelos pontos dos editais, separa por tipo (legislação, súmulas, temas, jurisprudência, enunciados, doutrina, questões, anotações), detecta o que é repetido, complementar ou divergente e só incorpora depois da sua aprovação. O material é visto como um documento no estilo Word (Cambria 12, A4), editável, e exportável para Word (.docx) e PDF.

## Arquivos do repositório

| Arquivo | Função |
|---|---|
| `index.html` | O aplicativo inteiro. |
| `editais.json` | Estrutura dos editais (TJSC 2025, TRF5 2026, TJRS 2026): 20 disciplinas e 800 pontos. |
| `lib/` | Bibliotecas locais: leitura de PDF (pdf.js), leitura de Word (mammoth) e geração de .docx (docx). |
| `manifest.json`, `icone*` | Permitem instalar como aplicativo no tablet e no celular. |

## 1. Publicar no GitHub Pages

1. Crie um repositório (ex.: `catedra`) e envie todos os arquivos desta pasta, mantendo a pasta `lib/`.
2. No repositório: Settings → Pages → Source: *Deploy from a branch* → Branch `main`, pasta `/ (root)` → Save.
3. Em um ou dois minutos o endereço fica disponível: `https://SEU-USUARIO.github.io/catedra/`.
4. No iPad ou no celular, abra o endereço no Safari/Chrome e use "Adicionar à Tela de Início".

No plano gratuito, o GitHub Pages exige repositório público. Por isso o seu material NÃO fica nesse repositório: ele vai para um segundo repositório, privado (passo 2).

## 2. Sincronizar PC, tablet e celular

1. Crie um segundo repositório, PRIVADO, por exemplo `catedra-dados` (pode deixá-lo vazio, com um README).
2. Crie um token: github.com → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token.
   - Repository access: *Only select repositories* → `catedra-dados`.
   - Permissions → Repository permissions → *Contents: Read and write*.
3. No Cátedra: Configurações → Sincronização → preencha usuário, repositório (`catedra-dados`), branch (`main`), arquivo (`catedra-dados.json`) e o token → Testar conexão → Sincronizar agora.
4. Repita o passo 3 em cada dispositivo. A partir daí, cada alteração é enviada automaticamente e cada abertura do aplicativo baixa o que mudou. Em conflitos, prevalece, item a item, a edição mais recente.

O arquivo `catedra-dados.json` é o seu banco de dados completo e pode ser baixado a qualquer momento (também há Configurações → Exportar backup).

## 3. Chave de API

- Claude: console.anthropic.com → Settings → API Keys. Recomendado.
- Gemini: aistudio.google.com → Get API key.

Informe a chave em Configurações. Em "Listar" você vê os modelos disponíveis na sua conta e pode fixar um; em "Automático", o app usa o Sonnet mais recente (Claude) ou o Pro mais recente (Gemini). As chaves e o token ficam só no navegador de cada dispositivo e nunca vão para o GitHub nem para o backup.

## 4. Fluxo de uso

1. Inserir material: cole o texto ou envie PDF, Word, TXT ou HTML. Indique a disciplina (ou deixe a IA detectar) e, se quiser, uma orientação ("tudo é jurisprudência do STJ").
2. A IA recorta o conteúdo em unidades, classifica tipo, assunto e ponto em cada edital, e compara com o que você já tem (busca local por semelhança + mesma súmula/tema/enunciado).
3. Triagem: cada unidade vem marcada como Novo, Complementa, Diverge ou Repetido, com a decisão sugerida (incluir, mesclar a informação nova no item existente, substituir ou descartar). Você altera título, referência, assunto, disciplina, pontos, texto e decisão; depois clica em "Aplicar decisões".
4. Caderno: escolha a disciplina e a lente do edital (TJSC, TRF5 ou TJRS, no alto). O documento segue a ordem dos pontos; dentro de cada ponto, agrupa por tipo e assunto (ou por assunto e tipo). Clique no texto para editar; a barra traz itálico, sublinhado, marca-texto, listas e citação recuada. Cada item tem classificação, destaque e exclusão.
5. Exportar: botões Word e PDF (disciplina inteira, só pontos com material, ponto atual ou pontos escolhidos). O Word sai com sumário automático: se aparecer vazio, clique com o botão direito sobre ele e escolha "Atualizar campo".

Leis penais especiais, execução penal e leis civis especiais têm disciplinas próprias; nos editais em que não são disciplinas autônomas, elas mostram os pontos correspondentes de Penal, Processo Penal e Civil (ex.: TJSC, Penal, pontos 50 a 79).

## 5. Atualizar os editais (`editais.json`)

- Pela interface: Editais → editar sigla, nome, cor e o texto de cada ponto, incluir ou excluir pontos, ou "Novo edital" (cole o conteúdo programático e a IA estrutura).
- Pelo arquivo: edite `editais.json` no repositório do site e aumente o número em `"versao"`. Ao abrir, cada dispositivo detecta a versão nova e atualiza a estrutura sozinho. Se você tiver editado editais pela interface, a tela Editais mostra um aviso para você decidir se substitui.
- Os identificadores dos pontos (`"id"`, ex.: `tjsc:civil:4`) são o vínculo entre o material e o edital: não os altere em pontos que já têm material.

## Limitações a conhecer

- A análise depende da IA: confira a classificação na triagem. O prompt proíbe inventar números de súmulas, temas e julgados e exige fidelidade ao texto, mas a revisão humana continua indispensável.
- Custos da API correm na sua conta do provedor. A tela de inserção mostra uma estimativa de tokens antes de enviar.
- PDF digitalizado (imagem) não tem texto extraível: o app envia o PDF diretamente à IA (até cerca de 100 páginas / 30 MB por arquivo). Para livros maiores, informe o intervalo de páginas.
- Sem sincronização configurada, os dados ficam só no navegador daquele dispositivo. Faça backups periódicos (Configurações → Exportar backup) ou ative a sincronização.
- Abrir o `index.html` direto do disco funciona no PC, mas a leitura de PDF e a exportação para Word podem ser bloqueadas por alguns navegadores fora de um endereço http(s). Use o endereço do GitHub Pages.
