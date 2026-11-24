# ⛽ Combustível

App simples para controlar o combustível do carro: **quanto gastei no mês, quantos litros, quantos km rodei e a média (km/L)**.

👉 **Abrir o app:** https://marcelohbuzeli.github.io/combustivel/

- Funciona no navegador do iPhone, sem instalar nada.
- Os dados ficam só no seu aparelho (nada vai para servidor).
- Média calculada pelo método do tanque: km rodados desde o último abastecimento ÷ litros abastecidos.
  A média aparece a partir do 2º abastecimento.

## Colocar na tela de início do iPhone

1. Abra o link acima no **Safari**.
2. Toque em **Compartilhar** → **Adicionar à Tela de Início**.

O ícone abre o app dentro do Safari. Isso é proposital: é o mesmo lugar onde o atalho do Apple Pay abre o app, então os dados ficam juntos.

## Registro automático pelo Apple Pay

Quando você paga com Apple Pay num posto, o iPhone abre o app com o **valor já preenchido** e pergunta só os **litros** e o **odômetro**.

Isso é feito com uma automação do app **Atalhos** (iOS 17 ou mais recente). Configure uma vez:

1. Abra **Atalhos** → aba **Automação** → **+** (Nova Automação).
2. Escolha **Transação**.
3. Selecione os cartões da Carteira que você usa no posto. Deixe os outros filtros como "Qualquer".
4. Marque **Executar Imediatamente** e toque em **Seguinte** → **Nova Automação em Branco**.
5. Adicione as ações, nesta ordem:
   1. **Corresponder Texto**: padrão
      `(?i)posto|combust|shell|ipiranga|petrobras|\bbr\b|\bale\b|raizen|graal|texaco`
      e no campo de texto escolha a variável **Comerciante** (do Atalho).
   2. **Se** → *Correspondências* → **tem qualquer valor**.
   3. Dentro do **Se**: **Codificar URL** com a variável **Quantia**.
   4. **Codificar URL** com a variável **Comerciante**.
   5. **Abrir URLs** com:
      `https://marcelohbuzeli.github.io/combustivel/?valor=`**[URL Codificada 1]**`&posto=`**[URL Codificada 2]**
6. Salve.

Pronto. Ao pagar num posto, toque na notificação (ou o Safari abre direto) e complete litros e odômetro.

**Dica:** se algum posto não for reconhecido, veja na Carteira como o nome dele aparece e acrescente uma palavra ao padrão do passo 5.1 (separada por `|`).

**Testar sem abastecer:** abra
https://marcelohbuzeli.github.io/combustivel/?valor=150,00&posto=Teste
e veja a tela que o atalho vai abrir (é só cancelar).

## Backup

O Safari pode apagar dados de sites que você não abre por muito tempo. Use **Exportar backup** de vez em quando (salva um arquivo `.json` no app Arquivos) e **Importar backup** para restaurar.
