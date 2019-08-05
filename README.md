
# AngularJS #1 - Introdução e Hello World

````
<!DOCTYPE html >
<html lang="en" ng-app="helloWorld">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Rodrigo Branas</title>
    <script src="angular.js"></script>
    
    <script>
        angular.module("helloWorld", []); // cria o módulo
        angular.module("helloWorld").controller("helloWorldController", function($scope){ // localizo o módulo e adiciono o $scope (ligar view ao controller)
                                                                                              // $scope porta de entrada pra view  
                $scope.message = "Hello world!";
        }); 
    </script>
</head>
<body>
    <div ng-controller="helloWorldController">
            {{message}}
    </div>
    
</body>
</html>
````


# AngularJS #2 - Usando Diretivas 

````
<!DOCTYPE html>

<html lang="en" ng-app="listaTelefonica">
<!--  ng-app -- define as fronteiras da aplicação  -->

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css"
        integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
    <title>Rodrigo Branas</title>
    <style>
        .jumbotron {
            width: 400px;
            text-align: center;
            margin: 20px auto;
        }

        th {
            text-align: center;
        }

        table {
            margin-top: 20px;
        }

        .form-control {
            margin-bottom: 10px;
        }
    </style>

    <script src="lib/angular.js"></script>
    <script>
        angular.module("listaTelefonica", []); // cria o módulo
        angular.module("listaTelefonica").controller("listaTelefonicaController", function ($scope) { // localizo o módulo e adiciono o $scope (ligar view ao controller)
            // $scope porta de entrada pra view  
            $scope.app = "Lista Telefonica";
            $scope.contatos = [
                { nome: "Pedro", telefone: "999999999" },
                { nome: "Ana", telefone: "000000000" },
                { nome: "Gabriel", telefone: "11111111" },
            ];

            // ⏩ FORMA 1
            // $scope.adicionarContato = function(){
            //     // console.log($scope.nome);   
            //     $scope.contatos.push({nome: $scope.nome, telefone: $scope.telefone }); // evitar ler $scope dentro do controler
            // }

            // ⌛ FORMA 2
            // $scope.adicionarContato = function(nome, telefone){
            //     // console.log($scope.nome);
            //     $scope.contatos.push({nome: nome, telefone: telefone }); 
            // }

            // 🌝 FORMA 3
            $scope.adicionarContato = function (contato) {
                // console.log($scope.nome);
                // $scope.contatos.push(contato); // forma mais correta
                $scope.contatos.push(angular.copy(contato)); // sem o angular.copy a tabela adicionada continua recebendo o bind
                delete $scope.contato; // remove o contato do input após deletar
            }
        }); 
    </script>
</head>

<body ng-controller="listaTelefonicaController">
    <div class="jumbotron">
        <!-- <h4 ng-bind="app"></h4> -->
        <h4>{{app}}</h4>
        <table class="table table-striped">
            <tr>
                <th>Nome</th>
                <th>Telefone</th>
            </tr>

            <tr ng-repeat="contato in contatos">
                <!-- ng-bind (do $scope para view) -->
                <td>{{contato.nome}}</td>
                <td>{{contato.telefone}}</td>
                <!-- OU -->
                <!-- <td ng-repeat="(key, value) in contato"> {{key + '-' + value}}</td> -->

                <!-- ngModel (do view para o $scope ) --- (aplico nos input,selects, textareas) -->
            </tr>
        </table>
        <hr>
        <!-- // ⏩ FORMA 1 + ⌛ FORMA 2  -->
        <!-- <input class="form-control" type="text" ng-model="nome" placeholder="Nome">
        <input class="form-control" type="text" ng-model="telefone" placeholder="Telefone"> -->

        <!-- 🌝 FORMA 3-->
        <input class="form-control" type="text" ng-model="contato.nome" placeholder="Nome">
        <input class="form-control" type="text" ng-model="contato.telefone" placeholder="Telefone">
        <!-- 
        two way data binding
        {{nome}}
        {{telefone}} 
        -->
        <!-- // ⏩ FORMA 1 -->
        <!-- <button class="btn btn-primary btn-block" ng-click="adicionarContato()">Adicionar Contato</button> -->

        <!-- ⌛ FORMA 2 -->
        <!-- <button class="btn btn-primary btn-block" ng-click="adicionarContato(nome, telefone)">Adicionar Contato</button> -->

        <!-- 🌝 FORMA 3-->
        <button class="btn btn-primary btn-block" ng-click="adicionarContato(contato)">Adicionar Contato</button>
        <!-- {{contato}} -->
    </div>

</body>

</html>

````

# AngularJS #3

````
https://www.youtube.com/watch?v=VcF7SySRkHs&list=PLQCmSnNFVYnTD5p2fR4EXmtlR6jQJMbPb&index=3

========================== ng-class ================================

<tr ng-class="{selecionado: contato.selecionado, negrito: contato.selecionado}" ng-repeat="contato in contatos">
OU
<tr ng-class="{'selecionado negrito': contato.selecionado}" ng-repeat="contato in contatos">




<table class="table">
    <tr>
        <th></th>
        <th>Nome</th>
        <th>Telefone</th>
        <th>Operadora</th>
    </tr>

    <tr ng-class="{selecionado: contato.selecionado}" ng-repeat="contato in contatos">
        <!-- ng-bind (do $scope para view) -->
        <td><input type="checkbox" ng-model="contato.selecionado"></td>
        <td>{{contato.nome}}</td>
        <td>{{contato.telefone}}</td>
        <td>{{contato.operadora.nome}}</td>
        <!-- OU -->
        <!-- <td ng-repeat="(key, value) in contato"> {{key + '-' + value}}</td> -->

        <!-- ngModel (do view para o $scope ) --- (aplico nos input,selects, textareas) -->
    </tr>
</table>


========================== ng-disabled ================================

 <button class="btn btn-primary btn-block" ng-click="adicionarContato(contato)" ng-disabled="!contato.nome || !contato.telefone">Adicionar Contato</button>


<!-- REMOVER CONTATOS--> 25 minutos

$scope.apagarContatos = (contatos) => {
        var contatosSelecionado =  contatos.filter((contato) => {
            if (contato.selecionado) return contato;
        });
        // console.log(contatosSelecionado);
        
}

$scope.apagarContatos = (contatos) => {
    $scope.contatos =  contatos.filter((contato) => {
        if (!contato.selecionado) return contato;
    });
}


$scope.isContatoSelecionado = (contatos) => { 
    var isContatoSelecionado =   contatos.some(function(contato) {
        return contato.selecionado; // se um dos contatos for true volta true e o botão habilita 
    });
    console.log(isContatoSelecionado);   
}


========================== ng-style ================================ 33 minutos

========================== ngShow, ngHide e ngIf ================================ 35 minutos

========================== ngInclude ================================ 39 minutos



````