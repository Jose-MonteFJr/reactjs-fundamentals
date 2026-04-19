# React Hooks

Permitem o uso de estados e outras funcionalidades do React em componentes funcionais, são serviços reutilizáveis, porém obrigatoriamente criados com funções, utilizamos para reaproveitamento e organização de código.   

Hooks principais: `useState`, `useEffect` e `useContext`.    

Hooks complementares: `useRef`, `useMemo`, `useCallback`, `useReducer`, `useTransition` e etc.

## Características 

- Sempre devem começar com a palavra `use` seguido do propósito dele. 

- Permite usar **estado**, **ciclos de vida**, **memorização** e outras funções nos componentes.

- Seguem a **regra de invocação**, devendo ser chamados no topo do componente.

> ⚠️ Os hooks **NÃO** podem ser executados dentro de loops, condições ou funções aninhadas.

- Tornam o código mais **reutilizável** e **organizado** com **hooks customizados**.

- Eliminam a necessidade do uso do "this", "bind" e etc. Facilitando a escrita e compreensão do código.

- São a base para a **abordagem moderna do React**, sendo amplamente usados em projetos recentes.

## React Hooks: Estados

O `useState` é um Hook do React que permite gerenciar o estado dentro de um componente funcional.

- Ele armazena um valor e fornece uma função para atualizá-lo, garantindo que o React saiba quando re-renderizar o componente.

- Você pode transportar valores das `props` para um estado e então eles serão mutáveis.

- Não há um limite de estados para um componente.

### Sintaxe 

- O `useState` recebe um valor inicial em seu parâmetro.

- Ele retorna uma **tupla**, sendo o primeiro índice o valor do estado e o segundo a função para atualizar o estado.

    - `useState(0)`: Define o estado inicial como `0`.

    - `contador`: Armazena o valor atual do estado.

    - `setContador`: Função usada para atualizar o estado.

- Quando o `setContador(novoValor)` é chamado, o componente re-renderiza automaticamente.

        function Counter() {
        const [counter, setCounter] = React.useState(0);
        
        return (
            <>
            <p>Contador: {counter}</p>
            <button onClick={() => setCounter(10)}>Atualizar</button>
            </>
        );
        }

### prevValue

Utilizado para validação com estado anterior ou para incrementação.

- Em uma atualização é possível utilizar o valor anterior do estado.

- Se o novo valor depender do estado anterior, passe uma função anónima que tem como primeiro parâmetro o prevValue.

## React Hooks: Condicionais

A **renderização condicional** no React permite exibir ou ocultar elementos com base em uma condição. Isso é útil para alternar interfaces, mostrar mensagens dinâmicas e etc.

> Para fazer condicionais podemos utilizar qualquer tipo de `if` do JS.

### Formas de utilizar condicionais 

- Operador ternário (`? :`) - Usado quando há duas opções possíveis.

        const [counter, setCounter] = React.useState(0);

        return (
        <>
            <p>{counter > 10 ? 'Maior que 10' : 'Menor ou igual a 10'}</p>
            <button 
            onClick={() => setCounter((prevValue) => prevValue + 1)}
            >
                Incrementar
            </button>
        </>
        );

- Curto-circuito (`&&`) - Usado quando só há um conteúdo a exibir caso a condição seja verdadeira.

        const [counter, setCounter] = React.useState(0);

        return (
        <>
            {counter > 15 && <p>Maior que 15</p>}
            <button 
            onClick={() => setCounter((prevValue) => prevValue + 1)}
            >
                Incrementar
            </button>
        </>
        );

- Tradicional (`if`) - Melhor para lógica mais complexa antes do retorno, caso a condição seja verdadeira, ignora tudo depois do return do `if`.

        const [counter, setCounter] = useState(0);

        if (counter > 20) {
            return <p>Maior que 20</p>
        } 

        return (
        <button 
            onClick={() => setCounter((prevValue) => prevValue + 1)}
        >
            Incrementar
        </button>
        );

> Essa regra se aplica também para renderização de outros componentes

## React Hooks: Listas (Arrays)

A **renderização de listas** no React é feita iterando sobre um array e gerando elementos dinamicamente.

O método mais comum é o `.map()`, mas também podemos usar o `.filter()` e outras funções de listas do JS para exibir apenas itens específicos.

> Para organizar e exibir listas podemos utilizar qualquer tipo de `Array Prototype` do JS.

### Formas de utilizar listas

- Renderizando listas com `.map()` - O meio mais fácil e comum.

        function ListNames() {
        const [names] = React.useState(["Ana", "Bruno", "Carlos"]);

        return (
            <ul>
            {names.map((name, index) => (
                <li key={`${index}-${name}`}>{name}</li>
            ))}
            </ul>
        );
        }

> ⚠️ Aqui utilizamos a propriedade `key` para organizar os elementos da árvore de renderização.   
>
> Não utilize apenas o "index" como chave.

- Filtrando valores com `.filter()` 

Podemos fazer um mix dos eventos com o método `filter` para listar apenas os nomes que batem com o campo de texto.

        function ListNames() {
        const [names] = React.useState(["Ana", "Bruno", "Carlos", "Daniel", "Eduarda"]);
        const [search, setSearch] = React.useState("");

        return (
            <div>
            <input
                type="text"
                placeholder="Buscar nome..."
                value={search}
                onChange={e => setSearch(e.target.value)}
            />
            <ul>
                {names
                    .filter(names => 
                        names.toLowerCase().includes(search.toLowerCase())
                    )
                    .map((name, index) => (
                    <li key={`${index}-${name}`}>{name}</li>
                    ))
                }
            </ul>
            </div>
        );
        }