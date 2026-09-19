# Sistema de apoio à decisão para o mini índice (WIN)

**Projeto de extensão — uso pessoal, sem fins lucrativos**  
Protótipo PWA (Android via Chrome → Adicionar à tela inicial)

## 1. Problema
O operador de mini índice (WIN) monta um checklist pré-market (futuros EUA, DXY, EWZ, ADRs, dólar) para estimar a probabilidade de *gap* na abertura. O erro mais comum é antecipar a entrada antes do fechamento da primeira vela de 15 minutos. Faltava um registro simples das sessões e uma consulta do tipo “dias como hoje”.

## 2. Objetivo
Disponibilizar um aplicativo de apoio — **sem execução automática de ordens** — que:
1. calcule hipótese de gap a partir de um score;
2. grave a sessão (abertura, 1ª de 15m, tipo de dia);
3. consulte a frequência histórica de padrões semelhantes.

## 3. Método
- Score de −2 a +2 em S&P, Nasdaq, Dow, Russell, VIX, DXY, EWZ, PBR, VALE, ITUB, BBD e USD/BRL.
- Soma → faixa de abertura (gap baixa / colado / gap alta).
- Filtro de lado: *close* da 1ª vela de 15m, não o pavio.
- Gatilho no gráfico de 5 minutos após 90 segundos.
- Padrão = tipo de gap + lado da 15m + tipo de dia (alta, baixa, range, varredura).
- Probabilidade = contagem / N da amostra. N &lt; 20 = estudo, não estatística.

## 4. Protótipo
Arquivos: `index.html`, `manifest.json`, `sw.js`.  
Abas: Pré-market · Histórico · Padrões · PEX.  
Amostra inicial: pregões de 03 a 18/09/2026. Importação CSV para base de 5 anos.

## 5. Resultado preliminar (amostra de setembro/2026)
Consultar no app a aba **Padrões** (filtro Gap BAIXA): o dia 10/09 é o contraexemplo didático — gap baixo que virou *varredura*, não venda automática.

## 6. Limitações e trabalhos futuros
- Amostra pequena até importar o histórico de 5 anos.
- Série antiga sem 15m deixa o campo de lado vazio.
- Mudança de regime (Selic, eleição) exige filtro por período.
- Evolução: API de cotações e tela nativa Kotlin. Fora do escopo deste PEX.

## 7. Conclusão
O sistema organiza o checklist já usado no dia a dia e transforma cada pregão em uma linha consultável. Não prevê o mercado; reduz a pressa de operar o gap sem o filtro de 15 minutos.
