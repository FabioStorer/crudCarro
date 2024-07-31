const prompt = require('prompt-sync')();
const carros = [];

let updateId = 1;

const modelo = (carroId) => {

    let carro = {
            carroNome: '',
            carroMarca: '',
            carroModelo: '',
            carroAno: '',
            carroPortas: '',
            carroId: ''
    };

    carro.carroNome = prompt('Digite o nome do carro: ');
    carro.carroMarca = prompt('Digite a marca do carro: ');
    carro.carroModelo = prompt('Digite o modelo do carro: ');
    carro.carroAno = prompt('Digite o ano de fabricação do carro: ');
    carro.carroPortas = prompt('Digite quantas portas o carro possui: ');
    
    if (carro.carroNome != '' && 
        carro.carroMarca != '' &&
        carro.carroModelo != '' &&
        carro.carroAno > 1950 &&
        carro.carroAno <= 2024 &&
        carro.carroPortas == 2 ||
        carro.carroPortas == 4) {
            carro.carroId = updateId
            updateId++;
            return carro;
        }
        console.log('Dados inválidos!');
    };

const criar = () => {
    
    const novo = modelo();
    
    if (novo) {
        carros.push(novo);
        console.log(carros)
        console.log('Carro cadastrado com sucesso!');
    }
};

const listar = () => {

    if (carros.length == 0) {
        console.log('Nenhum carro cadastrado.');
    }

    carros.forEach((el, index) => {
        console.log(`${index + 1}
            Nome do carro: ${el.carroNome}
            Marca do carro: ${el.carroMarca}
            Modelo do carro: ${el.carroModelo}
            Ano de fabricação do carro: ${el.carroAno}
            Quantidade de portas do carro: ${el.carroPortas}
            ID do carro: ${el.carroId}`);
    })
};

const atualizar = () => {

    listar();

    let index = prompt('Escolha pelo ID qual cadastro deseja atualizar: ') - 1;

    if (index != '' && index == 0 && isNaN(index)) {
        console.log('ID inválido!');
        if (index == carro.carroId || index >= 0) {
            const novo = modelo(index);
            carros[index] = novo;
            console.log('Cadastro atualizado com sucesso!')
        }
    }
};

const remover = () => {

    listar();

    const index = prompt('Escolha pelo ID qual cadastro deseja remover: ') - 1;

    if (index >= 0 && index < carros.length) {
        carros.splice(index, 1);
        console.log('Cadastro removido com sucesso!')
    } else {
        console.log('ID inválido!')
    }
};

module.exports = {
    criar,
    listar,
    atualizar,
    remover
};

#########################################################################################################################################

const prompt = require('prompt-sync')();
const funcao = require('./modules.js');

while (true) {

    console.log(`Escolha uma opção abaixo:
        1. Cadastrar
        2. Listar
        3. Atualizar
        4. Remover
        5. Finalizar`);
        const opcao = Number(prompt());

        switch (opcao) {

            case 1:

            funcao.criar();
                
                break;
        
                case 2:

                funcao.listar();
                
                break;
        
            case 3:

            funcao.atualizar();
                
            break;
    
            case 4:

            funcao.remover();
                
                break;
        
                case 5:

                process.exit();
                
                break;
        
            default:

            console.log('Opção inválida!');

                break;
        }
};
