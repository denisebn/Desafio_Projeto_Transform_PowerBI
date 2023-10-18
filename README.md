# Desafio_Projeto_Transform_PowerBI
Desafio de projeto 4 do Bootcamp Santander 2023 - Processando e Transformando Dados com Power BI usando banco de dados Azure

Passo a passo das etapas de transformação realizadas:

1- Cabeçalhos e tipos de dados ok.

2- Na tabela employee, foi modificado o tipo de dado da coluna salary para número decimal fixo.

3- O único nulo existente é no campo Super_ssn de um colaborador na tabela employee. A princípio esse campo é nulo mesmo e não deve alterar as análises, mas será verificado nas análises futuras.

4- para verificar se algum colaborador não tem gerente, mesclar a coluna de Super_ssn com snn na tabela employee, pois desse modo é possível ver qual o gerente de cada colaborador. Mantida somente as colunas Employee e Employee supervisor, as outras foram removidas. Tem somente um colaborador com um valor nulo como gerente, James. Seria ele o gerente geral? (tabela Employee and supervisor)
  
5 e 6- para verificar se todos os departamentos tem gerente, mesclar a tabela departments com a employee usando a coluna a identificação snn. Selecionar somente a coluna com o nome para verificar quem é o gerente de cada departamento, mantendo somente a coluna Department e Department supervisor. As outras foram excluídas. Todos departamentos possuem gerente. (tabela Supervisor by departament)

7- número de horas dos projetos: na tabela work_on, agrupar por Pno mostrando na segunda coluna Total hours a soma da coluna Hours. Para saber o nome do projeto e o departamento, mesclar com a tabela projects, mostrar somentes as colunas Project name e Department. Retirar linhas duplicadas. Organizando em ordem descrescente por Total hours é possível ver que os projetos Newbenefits e Computerization são os que possuem mais horas, com 55 horas total. (tabela hour by project)

8- dividindo a coluna Address da tabela employee em várias colunas. Primeiro realizar uma divisão usando delimitador personalizado "-" da extrema esquerda, deste modo uma coluna com o address number é criada. Depois realizar outra divisão da coluna Address restante, desta vez usando delimitador personalizado "-" da extrema direita, obtendo a coluna com o State. Como só tem nome de cidades com uma palavra, realizando mais uma divisão de colunas do Address restante, é possível separar a coluna City. Desta maneira, a coluna Address inicial foi separada em outras 4 colunas: address number, address, city e state. (Nota: as novas colunas adicionadas também apareceram nas tabelas mescladas que usavam a tabela employee, sendo necessária sua remoção para continuar com os dados desejados)

9 e 10- Criada a tabela Employee and departments mesclando a tabela employee usando a coluna Dno como referência com a tabela department e a coluna Dnumber. Se usar a tabela department como referência, os dados da tabela employee que serão adicionados nela. Selecionado para adicionar somente a coluna com o Dname. Foram mantidas na tabela somente as colunas Employee e Department, as outras colunas foram removidas.

11- a junção de colaboradores com seus respectivos gerentes já foi realizada na tabela Employee and supervisor, usando a mescla entre a colunas Super_snn com snn na tabela employee. Ver item 4.

12- mesclar a coluna com nome e sobrenomes dos colaboradores: selecionar as colunas Fname, Minit e Lname, ir em transformar > mesclar colunas. Escolher o separador como espaço e nomear a nova coluna como Employee. A coluna Fname foi renomeada Fname2 e a coluna Employee como Fname, para ser usada nas outras consultas. Não foi possível remover as colunas Fname, Minit e Lname pois estão sendo utilizadas em outras consultas.
