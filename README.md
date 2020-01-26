#Manual PDO Simples

#Fazer conexão com um banco em PDO

<?php
#Forma simples de fazer uma conexão PDO
$PDO = new PDO("<ODBC>:host=<maquina>;port=<porta>;dbname=<tabela>", "usuario do banco", "senha do banco");
?>

#Chamar informação com um UTF configurado

<?php
#Forma simples de fazer uma conexão PDF
$PDO = new PDO("<ODBC>:host=<maquina>;port=<porta>;dbname=<tabela>;charset=utf8", "usuario do banco", "senha do banco");
?>

* Neste caso chamei com o UTF8 configurado, lembre-se o banco tem que aceitar o Charset escolhido.

#Testar conexao banco

<?php
#Apresenta erro se não conectar
try {
    $PDO = new PDO("<ODBC>:host=<maquina>;port=<porta>;dbname=<tabela>;charset=utf8", "usuario do banco", "senha do banco");
} catch (PDOException $error) {
    echo $error->getMessage();
}
?>

#Colocar variáveis no local do texto do banco não fazer diferença, ai é mais questão de segurança e/ou manutenção

<?php

#uso de variaveis

$banco = "<ODBC>:host=<maquina>;port=<porta>;dbname=<tabela>;charset=utf8";
$usuario = "usuario do banco";
$senha = "senha do banco";

try {
    $PDO = new PDO($banco, $usuario, $senha);
} catch (PDOException $error) {
    echo $error->getMessage();
}
?>

#Como fazer um select

<?php
#select em PDO
$PDO->query('select * from tabela');
?>

#Fazer um count dos valores de uma query

#Pode fazer o padrão

<?php
#Conta a quantidade de valores trasidos pelo select
$PDO->query('select count(*) from tabela');
?>

#Ou usar o rwoCount() para contar o select

<?php
#Conta a quantidade de valores trasidos pelo select
$PDO->query('select * from tabela')->rowCount();
?>

#Como fazer um Insert, Update e Delete

<?php
#Pode ser qualquer uma dessas operações acima, o que muda é o SQL
#prepare usada usa os valores do execute para fazer o comando
$PDO->prepare('insert into tabela values(?,?,?)')->execute(['t1', 't2', 't3']);

#Use ? ou :nomeVariavel dentro do SQL
#No campo execute, você pode colocar um array ou os valores como acima

$PDO->prepare('insert into tabela values(:valor1,:valor2,:valor3)')->execute($array);

?>

#Pode usar o Try Catch para confirma se a operação foi um sucesso ou não

<?php
#Apresenta erro se não conectar
try {
    $PDO->prepare('insert into tabela values(?,?,?)')->execute(['t1', 't2', 't3']);
} catch (PDOException $error) {
    echo $error->getMessage();
}
?>