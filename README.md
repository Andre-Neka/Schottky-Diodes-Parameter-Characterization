# Extração de Parâmetros Físicos de Diodos Schottky (I-V e C-V)

Código em Python para extrair parâmetros físicos de diodos Schottky a partir de medidas experimentais estáticas de Corrente-Tensão ($I\text{-}V$) e Capacitância-Tensão ($C\text{-}V$), seguindo a metodologia analítica de Fu et al. (2014).

## O que o código calcula

A partir das curvas $I\text{-}V$ e $C\text{-}V$, o script faz as regressões lineares necessárias e propaga as incertezas ($\pm 1\sigma$) para obter:

* **Da curva $I\text{-}V$ direta:** fator de idealidade ($n$), corrente de saturação ($I_s$), inclinação ôhmica ($S_1$) e resistência da região de deriva ($R_D = 1/S_1$). Inclui um filtro opcional para descartar pontos travados no *compliance* do equipamento.
* **Da curva $C\text{-}V$ reversa:** inclinação $S_2$ via linearização de Mott-Schottky ($1/C_r^2 \times V_r$).
* **Parâmetros do dispositivo:** concentração média de dopantes ($N_D$), espessura da camada de deriva ($L_D$), área ativa efetiva ($A$) e altura de barreira Schottky ($\varphi_b$).
* **Perfil espacial:** largura da região de depleção $W_R(V_r)$ e perfil de dopagem $N_D(W_R)$ suavizado com filtro de Savitzky-Golay.

## Estrutura

* **Classes de materiais:** propriedades a $300\,\text{K}$ ($\varepsilon_r$, $\mu_{300}$, $E_{\text{gap}}$, $A^*$) já definidas para `silicon_carbide` (4H-SiC), `silicon` (Si), `gallium_nitride` (GaN), `gallium_arsenide` (GaAs), `germanium` (Ge) e `diamond` (C).
* **Funções de extração e plotagem:** separadas por etapa (`carregar_dados_experimentais`, `extrair_parametros_iv`, `extrair_parametros_cv`, `calcular_parametros_fisicos`, `calcular_perfil_deplecao` e `plotar_resultados`).

## Como rodar

1. Instale as bibliotecas necessárias:

```bash
pip install numpy pandas matplotlib scipy openpyxl
