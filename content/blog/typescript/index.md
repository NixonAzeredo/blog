---
title: Typescript
date: "2021-12-05T20:16:00.284Z"
description: "Um superset para javascript"
---

![typescript](./type.jpeg)

### O que é ?

TypeScript é um superconjunto de JavaScript desenvolvido pela Microsoft que adiciona tipagem e alguns outros recursos a linguagem.

### Vantagens ?

Além de simplificar a tipagem do código tornando mais acertivo e menos suscetível ao erro ainda podemos testar no ambiente de desenvolvimento em vez de rodar o código e ver os erros pelo console do navegador, o TypeScript ainda permite que utilizemos de funcionalidades da linguagem que ainda não estão disponíveis de forma nativa, por exemplo, no Node.js podemos utilizar os ES Modules (import/export) normalmente.

Outro ponto bem legal é que podemos transpilar nosso código para que o mesmo seja lido por todas versões de browsers, assim como fazemos com o Babel em aplicações totalmente JavaScript.

### Desvantagens ?

O typescript necessita de uma curva de aprendizado que não é longa e logo pode ser superada, mesmo que ainda seja javascript tem certas vatagens que no começo você pode não enterder porque a syntax é diferente do javascript, mas com certeza com o tempo você irá colher esse esforço!

### Como começar ?

Antes de qualquer coisa instale o typescript

```tsx
Tem duas formas de você instalar o typescript

Via NPM
npm install -g typescript

Via NPX
npx tsc
```

Crie um arquivo typescript script via terminal

```tsx
touch index.ts
```

Após o arquivo ser criado digite o código a seguir dentro desse arquivo e salve

```tsx
const welcome = 'Hello World';
console.log(welcome);
```

Digite o código a seguir no terminal.

```tsx
tsc  —init
O código acima serve para inicar uma configuração typescript, nele tem todas as
configurações que você irá precisar

tsc index.ts
Esse por sua vez transpila o seu arquivo ts em js, lembre-se o navegador não entende
typescript então você sempre irá precisar transpilar para js compatível com o navegador
```

Parabéns você acaba de criar seu primeiro código em typescript! 

OBS:  Agora você deve estar se perguntando o porque apareceu um arquivo javascript na sua pasta, ele é o código transpilado do typescript que você esqueveu.

Pronto, agora que quebramos o gelo vou apresentar a seguir alguns exemplos de uso do typescript. Esses exemplos são os mais usados no cotidiano de um desenvolvedor typescript.

OBS: No typescript não é necessário tipa tudo.

# Basics type

Para que os programas sejam úteis, precisamos ser capazes de trabalhar com algumas das unidades de dados mais simples: números, strings, estruturas, valores booleanos e assim por diante. No TypeScript, suporta os mesmos tipos que você esperaria em JavaScript, com um tipo de enumeração extra adicionado para ajudar nas coisas.

REF : [https://www.typescriptlang.org/docs/handbook/basic-types.html](https://www.typescriptlang.org/docs/handbook/basic-types.html)

```tsx
boolean => true/false;

string => 'foo', "foo", `foo`;

number => 3, 3.33, 0xff0, 00011100 => int, float, hex, binary;

array => number[], string[], object[] => type[] => Array<number>, Array<string>;

tuple => [number, string]; <= Array onde eu sei a quantidade e tipo;

x = ["hello", 10]; // ERRO
x = [10, "hello"]; // OK

enum => enum Colors {
	white = '#fff',
	black = '#000'
} => Valor e chave, serve para criar conjunto de chave e valor 
para chamada mais fácil;

any => Qualquer coisa;

void => Tipo vazio;

Null => Quando o valor é nulo;

Undefined => Valor não definido;

type => Criar um tipo novo que não seja um primtivo => type elias => 
ex: type Bla = string | undefined;

never => Nunca terá um retorno => Usado para excessões => ex:
	function error(): never {
	throw new Error('error');
};

object => Qualquer coisa que não seja esses tipos primitivos => 
 string, array, boolean, number ;

```

# Type inference

É quando a variável é criada já definindo seu tipo.

REF: [https://www.typescriptlang.org/docs/handbook/type-inference.html](https://www.typescriptlang.org/docs/handbook/type-inference.html)

```tsx
let message = "Mensagem definida" ;

message = 2 ; => Error => `Esse tipo já está definido como string` ;

message = "Novo"; => Success => `Sucesso pois o novo valor compartilha
do mesmo tipo do valor original`; 
```

## Union

É quando uma variável pode receber dois tipos, como exemplificado abaixo o parâmetro "uid" está recebendo valores tanto number quanto string. Para utilizar o Union basta adicionar um pipe entre os tipos.

REF: [https://www.typescriptlang.org/docs/handbook/advanced-types.html](https://www.typescriptlang.org/docs/handbook/advanced-types.html)

```tsx
logDetails(uid: number | string, item: string){
	console.log(`A product with ${uid} has a title as ${item}.`);
};
```

## Type Aliases

É quando se tem a necessidade de criar um tipo personalizado. Com Aliases pode condensar vários tipos em um único tipo.

```tsx
type Uid = number | string | undefined;

logDetails(uid: Uid, item: string){
	console.log(`A product with ${uid} has a title as ${item}.`);
};
```

## Type Aliases with Type inference

É quanto precisa seta tanto o tipo quanto valores específicos, desta forma mesmo se utiliza parâmetros do tipo string, não irá funcionar se o parâmetro não condizerem com os valores fornecidos na criação do tipo.

```tsx
type Platform = 'Windows' | 'Linux' | 'Mac Os'

function renderPlatform(platForm: Platform){
	return platForm;
};

renderPlatform('ios') <= Error
renderPlatform('Linux') <= Success
```

## Type Aliases with intersection

É quando se cria um tipo novo unindo outros dois tipos já existente, nesse caso se cria uma interseção de tipos, resultando assim um novo tipo com todas as propriedades dos tipos unificados.

```tsx
type AccountInfo ={
	id: number | string;
  name: string;
	email?: string, 
};

`OBS: o tipo email está como option que significa que pode tanto ser uma 
 string quando um undefined`

type CharInfo = {
	nickname: string;
	level: number;
};

const account: AccountInfo ={
	id: 123,
	name: "Fulano"
};

const char: CharInfo = {
	nickname: "fulanosilva",
	level: 100
};

` Intersection `

type PlayerInfo = AccountInfo & CharInfo;

const player: PlayerInfo = {
	id: '123',
	name: 'Bertano',
	nickname: 'bertanosilva',
	level: 100
};
```

# Classes

Classes em JavaScript provêm uma maneira mais simples e clara de criar objetos e lidar com herança. Vamos ver como elas funcionam em typescript

REF: [https://www.typescriptlang.org/docs/handbook/classes.html](https://www.typescriptlang.org/docs/handbook/classes.html)

```tsx
abstract class UserAccount {
  public name: string;
  protected age: number;

  constructor(name: string, age: number){
    this.name = name;
    this.age = age;
  }

  logDetails(): void {
    console.log(`The player ${this.name} is ${this.age} years old.`)
  }
}

class CharAccount extends UserAccount {
  private nickname: string;
  level: number;
	readonly email?: string;

  constructor(name: string, age: number, nickname: string, level: number){
    super(name, age); // <= Função para obter as propriedades da classe extendida;
    this.level = level;
    this.nickname = nickname;
  }

  get getLevel(): number{
    return this.level;
  }

  set setLevel(level:number){
    this.level = level;
  }

  logCharDetails(): void{
    console.log(`The player ${this.name} is ${this.age} and has the char ${this.nickname}
		 at level ${this.level}
    `);
  }
}

const john = new CharAccount('John', 45, 'johnmaster', 80);

console.log(john);

john.logDetails();

john.logCharDetails();

john.setLevel = 90;

console.log(john.getLevel);
```

super() ⇒ Função necessária para obter propriedades que estão sendo extendidas.

## Definições para acesso das propriedades fora da classe.

- readonly ⇒ É usado para somente permitir a leitura da propriedade na classe, entretanto, não pode alterar essa propriedade.
- private ⇒ É usado para bloquear leitura e gravação de fora da classe.
- public ⇒ É usado para permitir leitura e gravação de fora da classe.
- protected ⇒ É usado para permitir leitura e gravação apenas para subclasses ( Classes que extendem á classe dona da propriedade protegida)

## Accessors (Getter and Setter)

- Getter ⇒ Serve para retornar valores e propriedades da classe.
- Setter ⇒ Serve para definir valores e propriedades da classe.

## Abstract class

É um classe abstrata onde não é possível criar objetos a partir dela, mas é possivel extender suas propriedades para outra classe. Muito útil para criar modelos para outras classes.

# Interfaces

O que é: Conjunto de dados para descrever a estrutura de um objeto. ( Somente objetos )

Para que serve: Descrição de objetos mais complexos.

```tsx
interface Game { // Interface
  id?: string | number; // Optional and union 
  title: string; // Basic type
  description: string; // Basic type
  readonly genre: string; // Modifies
  platform?: string[]; // Optional
  getSimilars?: (title: string) => void; // Method signature
};

const tlou: Game = { // Define an object
  id: 123,
  title: 'The Last of Us',
  description: 'The best game in the world',
  genre: 'Action',
  platform: ['PS3', 'PS4'],
  getSimilars: (title: string) => {
    console.log(`Similar games to ${title}: Uncharted, A Plague tale, Metro`);
  }
};

if(tlou.getSimilars){ // Type Guard
  tlou.getSimilars(tlou.title);
};

interface DLC extends Game { // Interface extends another interface
  originalGame: Game;
  newContent: string[];
};

const leftbehind: DLC = { // Define an object with extends
  title: 'The Last of US - Left Behind',
  description: 'You Play as Ellie before the original game',
  genre: 'Action',
  platform: ["PS4"],
  originalGame: tlou,
  newContent: ['3 hours story', 'new characters']
};

class CreateGame implements Game { // Class implements an interface
  title: string;
  description: string;
  genre: string;

  constructor(t: string, d:string, g:string){
    this.title = t;
    this.description = d;
    this.genre = g;
  }
}
```

# Type Alias vs Interface

## Type Alias

Definição: 

```tsx
type Game = {
	title: string;
}

type DLCT = {
	extra: string;
}
```

Intersection:

```tsx
type GameCollection = Game & DLCT;
```

Implements:

```tsx
class CreateGame implements GameCollection { }
```

Declarar função:

```tsx
type getSimilars = (title:string) => void;
```

Permite declarar tipos primitivos:

```tsx
type IDT = string | number;
```

Permite declarar tuplas:

```tsx
type Tuple = [number, number];

[ 1 , 2 ] as Tuple; // <= Right
[ 1 , 2 , 3 ] as Tuple; // <= Error
```

Declarações:

```tsx
type JQuery = {
	a: string;
}

type JQuery = { // <= Error
	b: string;
}

"Type Alias não pode ter a mesma declaração"
```

## Interface

Definição: 

```tsx
interface Game{
	title: string;
}

interface DLC {
	extra: string;
}
```

intersection | extend:

```tsx
interface GameCollection extends Game, DLC {}
```

Implements:

```tsx
class CreateGame implements GameCollection { }
```

Declarar função:

```tsx
interface getSimilars {
	(title:string) => void;
}
```

Permite declarar tipos primitivos:

```tsx
"Interface não suporta declaração de tipos primitivos"
```

Permite declarar tuplas:

```tsx
interface Tuple { 
	0: number;
	1: number;
}

[ 1 , 2 ] as Tuple; // <= Right
[ 1 , 2 , 3 ] as Tuple; // <= Right
[ 1 , 2 , 3 , 'we'] as Tuple; // <= Right

"Todos os Exemplos funcionam na interface porque não tem como definir tuplas"
"Interface não suporta tuplas"
```

Declarações:

```tsx
type JQuery = {
	a: string;
}

type JQuery = {
	b: string;
}

const $: JQuery = {
	a: "bla",
	b: "foo"
}

"Interface permite múltiplas declarações e ele une de mesmo nome";

`OBS: Isso se torna uma vantagem quando for 
criar uma biblioteca porque são mais extensíveis!`;
```

### Em resumo, Type Alias vs Interface

As duas formas de tipagem são boas com pequenas diferenças, mas quando usar qual?.

1. Busque usar a interface para programar no padrão (POO) objetos/classes. ( Para criar objetos e classes mais complexas ).
2. Busque usar Alias para coisas simples e mais rápidas. ( Objetos menos complexos e tipos primitivos ).

Mas fique atendo! Com a padronização do seu projeto você deve manter a consistência, se seu projeto já usa um Alias para a maioria das coisas, então use ele sempre e use a interface somente em casos realmente necessários.

# Generics

Para que serve: Para ter mais flexibilidade no tipo e facilitar a reutilização de código.

```tsx
// S => State
// T => Type
// K => Key
// V => Value
// E => Element

type numOrStr = number | string;

function useState<S extends numOrStr = string>(){ //extends type and set default
    let state: S;

    function getState(){
        return state;
    };

    function setState(newState: S){
        state = newState;
    };

    return {getState, setState};
}

const newState = useState();

newState.setState("foo"); "Success"

console.log(newState.getState());

newState.setState(123); "Error"
console.log(newState.getState());
```

# Type Utilities

Documentação: 

[Handbook - Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)

```tsx
type Todo = {
  title: string;
  description: string;
  completed: boolean;
};

// readonly => type utilities
const todo: Readonly<Todo> = {
  title: "Assistir Dark de novo",
  description: "Relembrar os detalhes",
  completed: false,
};

console.log(todo);

// todo.completed = true; Error

function updateTodo(todo: Todo, fieldToUpdate: Partial<Todo>) {
    // Partial type utilities, isso faz com que todas os paramêtros do tipo Todo sejam opcionais
    return { ...todo, ...fieldToUpdate }; // Spread operator
}

const todo2: Todo = updateTodo(todo, {
  completed: true,
});

console.log(todo2);

// Pick Pega algumas propriedades do type alvo.
// Indicado para quando que pegar poucas propriedades do typo alvo

type TodoPreview = Pick<Todo, 'title' | 'completed'>;

const todo3: TodoPreview = {
    title: "Fechar Ghost of Tsushima",
    completed: false
};

console.log(todo3);

// Omit omite algumas propriedades do typo alvo.
// Indicado para quando que pegar muitas propriedades do typo alvo

type TodoPreview2 = Omit<Todo, 'description'>; 

const todo4: TodoPreview = {
    title: "Fechar Ghost of Tsushima",
    completed: false
};

console.log(todo4);
```

# Decorators

Anotação que pode ser anexada á uma classe, parâmetro ou acesso.

## Class decorator

```tsx
// Factory

function Logger(prefix: string){
    return  (target: any) => {
        console.log(`${prefix} - ${target}`);
    }
};

@Logger('awesome')
class Foo{

}
```

```tsx
// Class decorator

function setAPIVersion(apiVersion: string){
    return (constructor: any) => {
        return class extends constructor {
            version = apiVersion
        }
    }
}

// decorator - anotar a versão da API
@setAPIVersion("2.0.0")
class API {

}

console.log(new API());
```

## Property decorator

Decorator para propriedade

```tsx
function minLength(length: number){
    return (target: any, key: string) => {
        let val = target[key]

        const getter = () => val;

        const setter = (value: string) => {
            if(value.length < 5){
                console.log(`Error: você não pode criar
                ${key} com tamanho menos que ${length}`);
            } else {
                val = value;
            };
        };
        Object.defineProperty(target, key, {
            get: getter,
            set: setter
        })
    };
};

class Movie {
    // validação - se for menor que 5 letras - error
    @minLength(5)
    title: string;

    constructor(t: string){
        this.title = t;
    }
}

const movie = new Movie('Interstellar');
console.log(movie.title);
```

## Method decorator

```tsx
// Method decorator

function delay(ms: number){
    return (target: any, key: string, descriptor: PropertyDescriptor)=>{
        const originalMethod = descriptor.value;

        descriptor.value = function (...args: any[]) {
            console.log(`Esperando ${ms}...`)
            setTimeout(() => {
                originalMethod.apply(this, args)
            }, ms);

            return descriptor;
        }
    }
}

class Greeter {
    greeting: string;

    constructor(g: string){
        this.greeting = g;
    }

    @delay(2000)
    greet(){
        console.log(`Hello ${this.greeting}`)
    }
}

const pessoinha = new Greeter("pessoinha!")
pessoinha.greet();
```

### E aí gostou? espero que sim! haha. Mas se ainda não conseguiu pegar o typescript continue praticando, é questão de tempo até fixar o conhecimento

Fonte: 
[https://www.typescriptlang.org/docs/handbook/](https://www.typescriptlang.org/docs/handbook/)
