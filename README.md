# Desafio_Projeto_Transform_PowerBI
Desafio de projeto 4 do Bootcamp Santander 2023 - Processando e Transformando Dados com Power BI usando banco de dados Azure

Passo a passo das etapas de transformação realizadas:
- para verificar se algum colaborador não tem supervisor, mesclei a coluna de Super_ssn com snn na tabela employee, pois desse modo é possível ver qual o supervisor de cada colaborador. Tem somente um colaborador com um valor nulo como supervisor, James. Seria ele o gerente? (tabela Employee e Supervisores)
  
- para verificar se todos os departamentos tem gerente, mesclei a tabela departments com a employee usando a coluna a identificação snn. Selecionei somente a coluna com a identificação e o nome para verificar quem é o gerente de cada departamento. Todos possuem gerente.
- 
