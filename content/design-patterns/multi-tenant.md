Permite que uma mesma aplicação atenda a diferentes clientes (tenant) de forma independente
Você pode ter um banco de dados por cliente, ou colocar o id do cliente nas tabelas para usa-las de forma compartilhada

Você ainda pode adotar uma abordagem mista, um cliente muito grande pode sobrecarregar o trafego afetando clientes menores, ou por questões de
compliance, um cliente pode exigir que ele fique em um banco de dados separado ou mesmo numa infra totalmente separada