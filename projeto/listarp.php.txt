<?php

header('Content-Type: application/json; charset=utf-8');

$servidor = "localhost";
$usuario = "root";
$senha = "";
$banco = "graficoprodutos";

$conexao = new mysqli($servidor, $usuario, $senha, $banco);

if ($conexao->connect_error) {
    die(json_encode([
        "erro" => "Erro na conexão com o banco"
    ]));
}

$sql = "SELECT cod, nome, quant, valor, foto FROM produtos";

$resultado = $conexao->query($sql);

$produtos = [];

while ($linha = $resultado->fetch_assoc()) {
    $produtos[] = $linha;
}

echo json_encode($produtos);

$conexao->close();

?>