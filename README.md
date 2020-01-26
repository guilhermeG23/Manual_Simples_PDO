# Manual PDO Simples

Manual simples de PDO, feito só para marcar algumas informações e métodos que achei para resolver meus problemas.

### Antes de tudo

Lembre-se, para o PDO funcionar, seu servidor deve prover essa função.

Necessita de:
* habilitar no PHP;
* Ter o driver PDO para fazer a comunicação dom o banco;

### Fazer conexão com um banco em PDO

Forma simples de fazer uma conexão ao banco com o uso de PDO.

```
<?php
#Forma simples de fazer uma conexão PDO
$PDO = new PDO("<ODBC>:host=<maquina>;port=<porta>;dbname=<tabela>", "usuario do banco", "senha do banco");
?>
```

### Chamar informação com um UTF configurado

Charset é a config de como o banco irá se comunicar com o PHP, isso afeta a forma da informação ser apresentada.

```
<?php
#Forma simples de fazer uma conexão PDF
$PDO = new PDO("<ODBC>:host=<maquina>;port=<porta>;dbname=<tabela>;charset=<charset>", "usuario do banco", "senha do banco");
?>
```
### Pode usar váriaveis?

Pode usar sim váraiveis, isso não afeta em nada, porém lembre da segurança e da manutenção. 

```
<?php

#uso de variaveis

$banco = "<ODBC>:host=<maquina>;port=<porta>;dbname=<tabela>;charset=<charset>";
$usuario = "usuario do banco";
$senha = "senha do banco";

$PDO = new PDO($banco, $usuario, $senha);

?>
```

### Testar conexao banco

Confirmar se o banco está conectando ajuda muito no debug.
PDOException ajuda a confirmar se ocorreu algum problema.

```
<?php

$banco = "<ODBC>:host=<maquina>;port=<porta>;dbname=<tabela>;charset=<charset>";
$usuario = "usuario do banco";
$senha = "senha do banco";

try {
    $PDO = new PDO($banco, $usuario, $senha);
} catch (PDOException $error) {
    echo $error->getMessage();
}
?>
```

### Como fazer um select?

Agora como fazer uma chamada em uma tabela, ou qualquer outra operação.
Os exemplos acima estão criando o $PDO que é a váriavel que está armazenando a conexão ao banco, usaremos isso nos proximos trechos.

```
<?php
#um select simples, somente necessita da funcao query para o mesmo ser executado
$PDO->query('select * from tabela');
?>
```

Para outros comando em SQL isso não vai mudar muito.

### Fazer um count no SQL

Pode-se fazer o padrão ou a forma do PDO, tudo depende de como você queira fazer.

```
<?php
#Forma comum de fazer um count via SQL
$PDO->query('select count(*) from tabela');

#Forma com o uso de rowCount() do PDO
$PDO->query('select * from tabela')->rowCount();
?>
```

### E o Insert, Update e Delete?

Não difere muito do select, somente precisa de um acressimo.
Utilizamos o $PDO para ainda realizar a comunicação, porém agora usamos o 'prepare' para o SQL no banco, o uso do execute é para carregar a váriavel e executar a função.

```
<?php
#Pode ser qualquer uma dessas operações acima, o que muda é o SQL
#prepare usada usa os valores do execute para fazer o comando
$PDO->prepare('insert into tabela values(?,?,?)')->execute(['t1', 't2', 't3']);

#Use ? ou :nomeVariavel dentro do SQL
#No campo execute, você pode colocar um array ou os valores como acima
$PDO->prepare('insert into tabela values(:valor1,:valor2,:valor3)')->execute($array);
?>
```

### Pode usar o Try Catch para confirma se a operação foi um sucesso ou não

O uso do try catch é valida para todas as situação que precisamos confirmar se uma operação será realizada com sucesso ou não.

```
<?php
#Apresenta erro se não conectar
try {
    $PDO->prepare('insert into tabela values(?,?,?)')->execute(['t1', 't2', 't3']);
} catch (PDOException $error) {
    echo $error->getMessage();
}
?>
```