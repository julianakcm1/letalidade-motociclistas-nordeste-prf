# Letalidade de motociclistas nas rodovias federais do Nordeste

Projeto final da disciplina de Ciência de Dados (UFAL).
Professor: Bruno Pimentel.
Autora: Juliana Karla de C. M. Baracho.

## Pergunta

Em quais situações um acidente de moto nas rodovias federais do Nordeste tem mais chance de terminar em morte? E onde a PRF e os órgãos de trânsito devem concentrar fiscalização, campanhas e obras?

## Base de dados

Dados abertos da Polícia Rodoviária Federal (PRF), arquivo de acidentes **agrupados por pessoa**, de 2021 a 2025 (uma linha por pessoa envolvida).

- Fonte: https://www.gov.br/prf/pt-br/acesso-a-informacao/dados-abertos/dados-abertos-da-prf
- O notebook baixa os cinco arquivos anuais sozinho, pelo `gdown`. Os dados não estão neste repositório.

Recorte usado: estados do Nordeste, pessoas em motocicleta, motoneta ou ciclomotor, condutor ou garupa, com estado físico informado. Ao final, a base tem 48.209 motociclistas, dos quais 3.895 morreram (8,1%).

## Hipóteses

- **H1:** o tipo de acidente é o fator mais associado à morte.
- **H2:** acidentes à noite e no amanhecer são mais letais que os de dia.
- **H3:** a diferença de letalidade entre os estados muda quando se considera o tipo de acidente, o horário e a via.

## O que o notebook faz

1. Baixa e junta os arquivos de 2021 a 2025.
2. Faz o recorte (Nordeste, motociclistas).
3. Limpa os dados: valores impossíveis de idade e de ano de fabricação viram vazio; os vazios são preenchidos com a mediana.
4. Cria variáveis: hora, fim de semana, faixa etária, idade da moto, se havia outro veículo.
5. Explora a letalidade por grupo, com qui-quadrado, V de Cramér, Mann-Whitney e correlação de Spearman.
6. Compara regressão logística e Random Forest, com validação cruzada estratificada e agrupada por acidente e validação temporal (treino em 2021–2023, teste em 2024–2025).
7. Calcula as razões de chances ajustadas (statsmodels), com intervalo de confiança de 95% e erro-padrão agrupado por acidente.
8. Resume as hipóteses e propõe três ações, cada uma com indicador e critério de sucesso.

## Principais resultados

- O tipo de acidente é o fator mais associado à morte (V de Cramér = 0,31). Na colisão frontal morrem 33,0% dos motociclistas acidentados; na queda, 3,9%.
- Entre 0h e 6h acontecem 7,1% dos acidentes, mas 19,4% das mortes. No amanhecer, a chance de morte é 2,65 vezes a do pleno dia, comparando acidentes parecidos.
- Em trecho rural de pista simples morrem 19,0% dos acidentados; em trecho urbano de pista dupla, 2,8%.
- Alagoas tem a 2ª maior letalidade bruta, mas, em igualdade de condições, não difere de Bahia, Paraíba, Sergipe e Piauí. O Maranhão continua 2,46 vezes mais letal que Alagoas.
- Regressão logística e Random Forest tiveram desempenho parecido (AUC de 0,84). A regressão logística foi a escolhida por encontrar mais mortes e por ser interpretável.

Os resultados mostram associação, não causa.

## Como rodar

O notebook foi feito no Google Colab, que já tem todas as bibliotecas usadas. Basta abrir `motociclistas_nordeste_PRF.ipynb` no Colab e rodar tudo (Ambiente de execução → Executar tudo).
