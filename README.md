# Análise de Áreas Ardidas 2024 — Distrito de Lisboa (Automação em Python/ArcPy)

**Autor:** Áureo Miguel Rodrigues de Almeida (20250797)
**Curso:** MSc Geographic Information Science and Systems, NOVA IMS · U.C. Programação Geoespacial (2026)

## Resumo

Automação, em Python com o módulo **ArcPy**, do processamento e análise de áreas ardidas no Distrito de Lisboa (2024), a partir de dados oficiais da Carta Administrativa Oficial de Portugal (CAOP) e de áreas ardidas do ICNF. O objetivo foi construir um fluxo de trabalho reprodutível — reduzindo para segundos um processo que, feito manualmente no ArcGIS Pro, demoraria horas — cumprindo os requisitos da unidade curricular (2 testes lógicos, 2 ciclos, múltiplas operações de geoprocessamento).

## O que o script faz

1. Filtra o Distrito de Lisboa a partir dos distritos de Portugal Continental (com teste lógico de validação)
2. Recorta (`Clip_analysis`) as áreas ardidas de Portugal pelo limite do distrito
3. Calcula a área geodésica de cada polígono ardido (hectares), via `UpdateCursor`
4. Recorta as freguesias do distrito
5. Interseta (`Intersect_analysis`) freguesias com áreas ardidas, identificando quais foram afetadas
6. Gera um relatório de texto automático com todas as estatísticas
7. Cria ficheiros de layer (`.lyrx`) prontos a abrir no ArcGIS Pro
8. Valida a análise e lista os ficheiros gerados (com um segundo teste lógico e ciclo)

```
python analise_areas_ardidas_lisboa.py
```

> **Nota:** o script foi escrito para correr dentro do ambiente Python do ArcGIS Pro (usa `arcpy`) e com caminhos de ficheiros locais fixos — ajustar as variáveis `ardida`, `distritos`, `freguesias` e `saida` no topo do script conforme a tua estrutura de pastas.

## Requisitos cumpridos (unidade curricular)

- **2 testes lógicos:** validação da existência do distrito filtrado; validação de qualidade dos resultados finais
- **2 ciclos (`for`):** cálculo de área por polígono (`UpdateCursor`); listagem dos ficheiros gerados (`enumerate`)
- **Operações de geoprocessamento:** `MakeFeatureLayer_management`, `Clip_analysis`, `Intersect_analysis`, `AddField_management`, `SaveToLayerFile_management`, cálculo de área geodésica

## Resultados (execução de referência)

- **33 áreas ardidas** identificadas no Distrito de Lisboa em 2024
- **167,91 hectares** de área total ardida
- **134 freguesias** no distrito, das quais **39 afetadas (29,1%)**
- **5,09 hectares** de área média por ocorrência
- Ganho de eficiência estimado: análise reduzida de horas (processo manual no ArcGIS Pro) para 15–20 segundos

## Dados utilizados

| Dataset | Fonte |
|---|---|
| Áreas ardidas 2024 (`ardida_2024.shp`) | ICNF |
| Distritos (`Cont_Dist_CAOP2022.shp`) | CAOP 2022, DGT |
| Freguesias (`Cont_Freg_CAOP2022.shp`) | CAOP 2022, DGT |

## Stack

Python · ArcPy · ArcGIS Pro · geoprocessamento vetorial (Clip, Intersect, cálculo de área geodésica)

## Nota

O relatório completo, com a descrição passo-a-passo do código, capturas de ecrã da execução (Visual Studio Code e ArcGIS Pro) e o código integral comentado em anexo, está incluído neste repositório (`relatorio.pdf`).
