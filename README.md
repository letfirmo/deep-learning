# 🧠 Redes neurais no arduino 🤖

## Índice
- [Visão Geral](#visão-geral)
- [Instalação](#instalação)
- [Referência](#referência)

## Visão geral

Utilização de redes neurais para a criação de uma estufa no Horto Florestal de Camaçari-BA, para que irrigue as plantas dependendo da temperatura e umidade do dia. 
Esta rede neural será a base do código que iremos criar para a estufa.

## Instalação
Iniciamos chamando a biblioteca <math.h> que permite o uso de funções matemáticas básicas na linguagem de programação C, como senos, cossenos, logaritmos, exponenciais, entre outras.
Após isso, declaramos as variáveis que vamos usar:
- PatternCount se refere ao número de itens de treinamento ou linhas na tabela verdade.
- InputNodes é o número de nós de entrada (há 7 valores em uma linha da tabela verdade).
- HiddenNodes é o número de nós escondidos. O arduino não consegue processar mais de 8 nós escondidos.
- OutputNodes é o número de nós de saída (há 4 valores de saída para cada linha na tabela verdade).
- LearningRate é a taxa de aprededizagem da rede, se ela aprenderá mais rápido, ou com maior qualidade.
- Momentum ajusta o quanto os resultados da iteração anterior afetam a iteração atual.
- InitialWeightMax define o valor inicial máximo para pesos.
- Success é o limite de erro no qual se diz que a rede resolveu o conjunto de treinamento.

```ino
#include <math.h>

const int PatternCount = 10;
const int InputNodes = 7;
const int HiddenNodes = 8;
const int OutputNodes = 4;
const float LearningRate = 0.3;
const float Momentum = 0.9;
const float InitialWeightMax = 0.5;
const float Success = 0.0004;
```
Agora vamos formar matrizes com arrays para colocar os dados de entrada e os dados de saída (esperados).
Observe que há 10 linhas (PatternCount) e 7 colunas (InputNodes).
```ino
const byte Input[PatternCount][InputNodes] = {
  { 1, 1, 1, 1, 1, 1, 0 },  // 0
  { 0, 1, 1, 0, 0, 0, 0 },  // 1
  { 1, 1, 0, 1, 1, 0, 1 },  // 2
  { 1, 1, 1, 1, 0, 0, 1 },  // 3
  { 0, 1, 1, 0, 0, 1, 1 },  // 4
  { 1, 0, 1, 1, 0, 1, 1 },  // 5
  { 0, 0, 1, 1, 1, 1, 1 },  // 6
  { 1, 1, 1, 0, 0, 0, 0 },  // 7 
  { 1, 1, 1, 1, 1, 1, 1 },  // 8
  { 1, 1, 1, 0, 0, 1, 1 }   // 9
}; 
```
Os arrays da saída (esperada) tem a mesma quantidade de linhas, mas apenas 4 colunas (OutputNodes).
```ino
const byte Target[PatternCount][OutputNodes] = {
  { 0, 0, 0, 0 },  
  { 0, 0, 0, 1 }, 
  { 0, 0, 1, 0 }, 
  { 0, 0, 1, 1 }, 
  { 0, 1, 0, 0 }, 
  { 0, 1, 0, 1 }, 
  { 0, 1, 1, 0 }, 
  { 0, 1, 1, 1 }, 
  { 1, 0, 0, 0 }, 
  { 1, 0, 0, 1 } 
};
```

## Referência
Código encontrado no site [Hobbizine](https://robotics.hobbizine.com/arduinoann.html), referente à playlist de Inteligência Artificial com Arduindo do canal Inteligência Mil Grau.

 [Assista à playlist no Youtube](https://www.youtube.com/playlist?list=PLYAGaVIlnsYaRibf94GEOwZh7qdCLcbJ5)
