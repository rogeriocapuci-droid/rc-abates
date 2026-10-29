# Manual do App Abate (Fechamento de Abate)

Este manual fica na pasta do app e deve ser mantido atualizado a cada mudança. Última atualização: versão 26, 29/10/2026.

## 1. O que tem nesta pasta

| Arquivo | Para que serve | Mexe? |
|---|---|---|
| `index.html` | O app inteiro (telas, cálculos, mensagem do WhatsApp, fontes). É o único arquivo que muda quando o app é atualizado. | Só trocando por uma versão nova |
| `sw.js` | Guarda o app no aparelho para abrir sem internet. O número em `VERSAO` sobe a cada atualização. | Só junto com o `index.html` |
| `manifest.webmanifest` | Nome e ícone do app quando é instalado na tela inicial. | Não |
| `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` | Ícones. | Não |
| `MANUAL.md` | Este manual. | Sempre que algo mudar |

## 2. Como os dados são guardados

- Os lançamentos ficam **somente no aparelho** (no navegador do iPhone). O app mostra "Só neste aparelho" no topo.
- Se o app for aberto em outro endereço, outro navegador ou outro aparelho, ele começa **vazio**. Os dados não passam sozinhos.
- Limpar os dados do Safari apaga os lançamentos. Por isso existe o backup.

### Backup (faça sempre antes de trocar de endereço ou de aparelho)
1. Na tela inicial do app, role até o quadro **Backup**.
2. Toque em **Salvar arquivo de backup** e mande o arquivo para o WhatsApp, iCloud ou Drive.
3. No app novo, toque em **Importar backup** e escolha o arquivo.
4. O app também guarda 1 cópia automática por dia, por 30 dias, no próprio aparelho. Em **Cópias automáticas** dá para restaurar (toque duas vezes para confirmar).

## 3. Como atualizar o app (o caminho normal)

1. Peça a mudança ao Claude, descrevendo o que quer ver na tela. Mande uma captura de tela quando ajudar.
2. O Claude altera o app e entrega o `index.html` novo (e o `sw.js` com o número de versão maior).
3. Troque os arquivos no GitHub:
   - Abra o repositório `rc-abates` no GitHub (site ou app).
   - Toque em **Add file** e depois **Upload files**.
   - Envie o `index.html` e o `sw.js` novos. Como têm o mesmo nome, o GitHub substitui os antigos.
   - Em **Commit changes**, escreva um resumo curto, por exemplo "v25 campo X", e confirme.
4. Aguarde 1 a 2 minutos (o GitHub Pages republica sozinho).
5. No iPhone, feche o app por completo e abra de novo. Na primeira abertura mostra a versão antiga e baixa a nova em segundo plano; na segunda abertura já aparece a nova. Se não mudar, abra e feche mais uma vez.

Quando o Claude tiver acesso de escrita ao repositório, ele envia direto, e os passos 3 e 4 deixam de ser seus.

## 4. Como voltar a uma versão anterior

1. No repositório, abra o `index.html` e toque em **History**.
2. Escolha a versão boa, abra o arquivo daquele momento e baixe com **Raw**.
3. Envie esse arquivo de volta com **Upload files**, ou peça ao Claude para restaurar.

Os dados dos lançamentos **não** voltam junto, porque ficam no aparelho e não no código.

## 5. Como instalar no iPhone

1. Abra o endereço do app no **Safari** (normalmente `https://rogeriocapuci-droid.github.io/rc-abates/`; confira o endereço exato em Settings > Pages do repositório).
2. Toque no botão de compartilhar e depois em **Adicionar à Tela de Início**.
3. Abra pelo ícone. Funciona sem internet.

## 6. Como pedir mudanças (exemplos)

- **Campo novo:** diga em que tela e em que bloco ele entra, em que ordem e se entra na mensagem do WhatsApp.
- **Corrigir conta:** dê um exemplo com os números que digitou e o resultado que esperava. Com o exemplo o erro se acha rápido.
- **Mudar aparência:** mande uma captura e diga o que ficou grande, pequeno ou no lugar errado.
- **Regra da mensagem:** diga qual linha entra, sai ou muda.

Depois de cada mudança, atualize a seção 9 (histórico).

## 7. Regras de cálculo usadas

- **Média na fazenda** = peso na fazenda ÷ cabeças.
- **Peso esperado** = peso na fazenda × rendimento esperado. **Esperado por cabeça** = peso esperado ÷ cabeças.
- **Carcaça:** pode ser digitada como total do lote ou média por cabeça. O app reconhece se o valor digitado parece ser de outro tipo e corrige sozinho (aparece um aviso).
- **Resultado:** carcaça real − peso esperado. Positivo é **lucro** (rendeu mais que o esperado), negativo é **prejuízo**. Aparece por cabeça e no lote.
- **Partes do lote:** quando o mesmo lote tem rendimentos diferentes (por exemplo 14 a 53% e 7 a 52%), cada parte tem as suas cabeças, peso e rendimento. O esperado é a soma das partes (até 5 partes no total).
- **% Fazenda** = carcaça ÷ peso da fazenda. **% Frigorífico** = carcaça ÷ peso de entrada.
- **Precoce:** só é precoce se passar de **60%** do lote (61 de 100 é precoce, 60 não é).
- **Valor da arroba:** 1 arroba = 15 kg de carcaça. **Valor do resultado** = kg de resultado ÷ 15 × valor da arroba.
- **Regras por frigorífico** (o app reconhece pelo nome digitado no campo Frigorífico):
  - **JBS** (Nova Andradina, Naviraí e qualquer nome com "JBS"): aparecem os campos **Prazo (dias)** e **Juros prazo (% ao mês)**. O prazo padrão é 30 dias e o juros padrão é 1,87% ao mês, que o app divide por 30 para achar o desconto por dia (0,0623% ao dia).
    - **Sem marcar "Adiantar pagamento":** o gado fica a prazo. Aparece só o **Valor a prazo**, sem desconto.
    - **Marcando "Adiantar pagamento":** aparece **Dias adiantados** (de 1 até o prazo). Desconto = valor do lote × juros ao dia × dias adiantados (juros simples). **Valor adiantado** = valor do lote − desconto. Mais dias que o prazo contam como o prazo.
    - O valor do lote é o que o pecuarista recebe pelo que foi acertado: carcaça total ÷ 15 × valor da arroba.
    - O **lucro não leva esse desconto**. O lucro de todos os lotes do dia 1 ao último dia do mês é somado e pago no **dia 15 do mês seguinte**. A ficha mostra "Lucro pago em 15/mm/aaaa" e o Histórico mostra o quadro **JBS · lucro por mês**.
  - **Zanchetta:** comissão de **10%** sobre o valor do lote (aparece também o valor por animal). Se estiver marcado **Peso vivo frigorífico** em "Conferir no abate", o frigorífico desconta **1,5%** do peso total (despesas dele) e **não paga comissão**. O app mostra o desconto em kg e o **Peso pago**.
  - **Outros frigoríficos:** só aparece o campo de arroba, sem prazo, juros ou comissão.
- Todos os números usam 2 casas decimais.

## 8. O que aparece onde

- **Lista "Pecuaristas do dia":** frigorífico, pecuarista, fazenda (letra pequena), cabeças, curral, sequência, médias, situação e resultado em kg e em R$.
- **Ficha do pecuarista:** bloco 1 (informação do abate, arroba/prazo/juros, rendimento, conferir no abate), bloco 2 (peso de entrada, sequência, curral), bloco 3 (carcaça e resultado).
- **Mensagem do WhatsApp:** só lotes com peso de carcaça. **Não leva** valor da arroba, prazo, juros nem valores em reais.
- **Histórico:** todos os abates, com busca por pecuarista, frigorífico, fazenda ou data, e legendas do que falta preencher.
- **Nomes salvos:** a setinha ▾ no campo Frigorífico ou Pecuarista abre a lista A a Z de nomes já lançados.

## 9. Histórico de versões

- **v26:** juros em % ao mês (1,87, dividido por 30 ao dia); prazo padrão 30 dias; regras por frigorífico (JBS: adiantamento e lucro pago dia 15 do mês seguinte; Zanchetta: comissão de 10% ou desconto de 1,5% no peso vivo); quadro de lucro por mês da JBS no Histórico.
- **v25:** "Adiantar pagamento" clicável: sem marcar o gado fica a prazo; marcando, informa os dias adiantados e calcula o desconto.
- **v24:** fazenda em letra pequena sob o nome; dados do lote menores na lista.
- **v23:** curral e sequência na lista do dia.
- **v22:** campos Prazo (dias) e Juros prazo (% ao dia) com desconto do adiantamento, na mesma linha da arroba.
- **v21:** valor da arroba e resultado em R$ (fora da mensagem).
- **v20:** setinha para abrir os nomes salvos de frigorífico e pecuarista.
- **v19:** campo Fazenda e currais na lista do dia.
- **Antes:** partes do lote com rendimentos diferentes, backup, versão instalável sem internet, histórico, conferir no abate, curral e sequência na ficha, regra do precoce e mensagem com rendimento, peso do frigorífico e resultado.

## 10. Problemas comuns

- **Não apareceu a mudança:** feche o app por completo e abra duas vezes. Se persistir, no Safari: Ajustes > Safari > Avançado > Dados de Sites > remover só o endereço do app (**faça o backup antes**, isso apaga os lançamentos).
- **Sumiram os lançamentos:** confira se abriu o mesmo endereço de antes. Se não, use a cópia automática ou o arquivo de backup (seção 2).
- **Tela em branco depois de atualizar:** suba de novo o `index.html` e o `sw.js` juntos, da mesma versão.
- **Número estranho no resultado:** confira se a carcaça está como total ou média (o app avisa quando corrige sozinho) e se o rendimento esperado está certo.
