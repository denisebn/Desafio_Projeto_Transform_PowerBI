# Desafio_Projeto_Transform_PowerBI
Desafio de projeto 4 do Bootcamp Santander 2023 - Processando e Transformando Dados com Power BI usando banco de dados Azure

Passo a passo das etapas de transformação realizadas:

1- Cabeçalhos e tipos de dados ok.

2- Na tabela employee, foi modificado o tipo de dado da coluna salary para número decimal fixo.

3- O único nulo existente é no campo Super_ssn de um colaborador na tabela employee. A princípio esse campo é nulo mesmo e não deve alterar as análises, mas será verificado nas análises futuras.

4- Para verificar se algum colaborador não tem gerente, mesclar a coluna de Super_ssn com snn na tabela employee, pois desse modo é possível ver qual o gerente de cada colaborador. Mantida somente as colunas Employee e Employee supervisor, as outras foram removidas. Tem somente um colaborador com um valor nulo como gerente, James. Seria ele o gerente geral? (tabela Employee and supervisor)
  
5 e 6- Para verificar se todos os departamentos tem gerente, mesclar a tabela departments com a employee usando a coluna a identificação snn. Selecionar somente a coluna com o nome para verificar quem é o gerente de cada departamento, mantendo somente a coluna Department e Department supervisor. As outras foram excluídas. Todos departamentos possuem gerente. (tabela Supervisor by departament)

7- Número de horas dos projetos: na tabela work_on, agrupar por Pno mostrando na segunda coluna Total hours a soma da coluna Hours. Para saber o nome do projeto e o departamento, mesclar com a tabela projects, mostrar somentes as colunas Project name e Department. Retirar linhas duplicadas. Organizando em ordem descrescente por Total hours é possível ver que os projetos Newbenefits e Computerization são os que possuem mais horas, com 55 horas total. (tabela hour by project)

8- Dividindo a coluna Address da tabela employee em várias colunas. Primeiro realizar uma divisão usando delimitador personalizado "-" da extrema esquerda, deste modo uma coluna com o address number é criada. Depois realizar outra divisão da coluna Address restante, desta vez usando delimitador personalizado "-" da extrema direita, obtendo a coluna com o State. Como só tem nome de cidades com uma palavra, realizando mais uma divisão de colunas do Address restante, é possível separar a coluna City. Desta maneira, a coluna Address inicial foi separada em outras 4 colunas: address number, address, city e state. (Nota: as novas colunas adicionadas também apareceram nas tabelas mescladas que usavam a tabela employee, sendo necessária sua remoção para continuar com os dados desejados)

9 e 10- Criada a tabela Employee and departments mesclando a tabela employee usando a coluna Dno como referência com a tabela department e a coluna Dnumber. Se usar a tabela department como referência, os dados da tabela employee que serão adicionados nela. Selecionado para adicionar somente a coluna com o Dname. Foram mantidas na tabela somente as colunas Employee e Department, as outras colunas foram removidas.

11- A junção de colaboradores com seus respectivos gerentes já foi realizada na tabela Employee and supervisor, usando a mescla entre a colunas Super_snn com snn na tabela employee. Ver item 4.

12- Mesclar a coluna com nome e sobrenomes dos colaboradores: selecionar as colunas Fname, Minit e Lname, ir em transformar > mesclar colunas. Escolher o separador como espaço e nomear a nova coluna como Employee. A coluna Fname foi renomeada Fname2 e a coluna Employee como Fname, para ser usada nas outras consultas. Não foi possível remover as colunas Fname, Minit e Lname pois estão sendo utilizadas em outras consultas.

13- Para descobrir a localização de cada departamento, foi feito um mesclar da tabela dept_locations com a tabela departments associando a coluna Dnumber de ambas. Na nova tabela obtida, foi mantioda somente a coluna com Department Name, Department Supervisor e Employee City. Deste modo é possível verificar se os gerentes moram na mesma cidade do departamento que gerenciam. Foi observado uma discrepância pois a colaboradora Jennifer S Wallace mora em Bellaire e gerencia o departamento Stafford Administration. (tabela Department location and supervisors)

14- Não foi usado o combinar em nenhum dos casos de mesclar, inclusive no item anterior, pois no combinar os dados da segunda tabela somente seriam inseridos na sequência da primeira tabela, em novas linhas, sem associar os valores em comum de ambas tabelas na mesma linha. Não é a informação esperada para fazer a análise.

15- Duplicando a tabela Employee and supervisors obtida no item 4, realizar um agrupamento pela coluna Employee Supervisor, gerando uma nova coluna com a contagem de linhas para descobrir quantos colaboradores possui cada gerente. (tabela Count employee by supervisor)

16- A eliminação das colunas desnecessárias já foi feita e indicada em cada uma das transformações feitas.

Para não gerar erro nas novas consultas, as tabelas originais foram mantidas pois há muitas consultas dependendo das colunas presentes nessas tabelas.

Para ir além:
17- Foram mescladas em uma única tabela as informações de Project, Project location, Project department, Hours, Employee, Employee city, Employee supervisor, Employee department e Department Supervisor. Essa tabela foi usada para analisar algumas situações:

18- Quantas horas cada colaborador está trabalhando nos projetos? Realizando um agrupamento por Employee e adicionando soma da coluna Hours, o resultado foi a tabela Hours by employee. Essa análise revelou que a distribuição de horas está igualitária entre os colaboradores, somente a Jennifer S Wallace que trabalha um pouco menos de horas que os demais colaboradores. Então pode-se concluir que não há sobrecarga de trabalho para ninguém. Também consta que o colaborador James E Borg possui nenhuma hora de envolvimento nos projetos. Pela tabela Employee and supervisor, é possível observar que esse colaborador é gerente dos outros gerentes de departamentos, logo podemos supor que ele é um gerente geral.

19- Em quantos projetos trabalha cada colaborador? Para verificar essa informação, um novo agrupamento foi feito por Employee contando o número de linhas. Foi obtida a tabela Project total by employee, que mostra que o colaborador que mais possui projetos é Franklin T Wong, envolvido em 4 deles, que é o dobro de projetos dos outros colaboradores. O que menos possui são os colaboradores James E Borg e Ramesh K Narayan. Desconsiderando James E Borge por ser gerente geral, verificando que o Ramesh K Narayan trabalha no mesmo departamento que Franklin T Wong, pode-se propor que Franklin passe um dos projetos para Ramesh (diferente do projeto que ele já está envolvido), ficando assim com menos projetos envolvidos. Para não haver sobrecarga para nenhum dos dois, o número de horas trabalhados em cada projeto deverá ser ajustado nesse caso.

20- Para descobrir em qual cidade-departamento cada um dos colaboradores trabalha, juntar a coluna Project location com Project deparment, obtendo um novo departamento composto por "cidade departamento" na coluna Project location depto. Mesclar a coluna Employee department com a coluna Dno da tabela Employee para recuperar o Department ID. Mesclar essa coluna Dno com a coluna Dnumber da tabela Department location and supervisors, recuperando a coluna Department location e renomeando como Employee department location. Adicionar uma nova coluna personalizada, usando a fórmula [Employee department location]=[Project location depto]. O resultado na coluna será True ou False. Filtrar para mostrar somente True, ou seja, mostrar somente os departamentos dos colaboradores que coincidem com os departamentos dos projetos. O resultado será os cidades-departamentos onde cada colaborador trabalha.

21- Um dado simples foi mostrar o nome dos colaboradores que possuem dependentes, mesclando a coluna Essn na tabela dependent com a mesma coluna na tabela employee e somente recuperar a coluna Fname.

Um relatório foi gerado sobre a análise de dados dos projetos e encontra-se publicado no Power BI Web [link](https://app.powerbi.com/groups/me/reports/7b678961-2d56-4599-bc37-64ca80231c92/ReportSection?experience=power-bi).
O arquivo power BI contendo todas as análises e tabelas descritas acima encontra-se nesse (repositório).

Qualquer dúvida é só entrar em contato por [email](denisebn@gmail.com).
