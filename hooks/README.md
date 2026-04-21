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

- São objetos ou variáveis especiais que armazenam dados dinâmicos de um componente

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

## React Hooks: API de contexto

A **Context API (ou store)** permite **compartilhar estados e funções** entre componentes **sem precisar passar props manualmente** de um componente para outro.

Utilizado quando precisa passar dados de filho para pai, ou em componentes em paralelo.

- Utilizar quando você tem vários componentes que precisam acessar o mesmo dado, como um **tema escuro/claro**, **usuário logado**, ou **configurações globais**.

- Sem Context API, seria necessário passar informações como props, de pai para filho, o que seria um **problema ao escalar**.

- Com Context API, criamos um **contexto (Context)** e um **"provedor" (Provider)** que pode ser acessado por qualquer componente na árvore.

### Características 

- Pode ter **múltiplos componentes de Context API** - eles não precisam necessariamente estarem disponíveis para a aplicação toda.

- Para utilizar dentro dos componentes, a Context API precisa estar como um **"wrapper"** deles.

- Os estados globais também utilizam o hool `useState` (ou outros hooks necessários).

- O React fornece duas funções para a criação e utilização: `createContext` e `useContext`

### Erros ao utilizar Context API

- Não utilize Context API para estados simples, nesses casos utilize `useState`, usar Context nesse caso pode ser um "overkill", `useState` estados locais, `Context API` estados globais.

- Performance: Usar apenas a Context API pode causar renders desnecessários na árvore.

### Como utilizar Context API

### 1. Criando o componente do contexto

        const CounterContext = React.createContext();

        function CounterProvider({ children }) {
        const [savedCounts, setSavedCounts] = React.useState([]);

        function saveCount(count) {
            setSavedCounts((prev) => [...prev, count]);
        }

        return (
            <CounterContext.Provider value={{ savedCounts, saveCount }}>
            {children}
            </CounterContext.Provider>
        );
        }

### 2. Integrar o contexto como um "wrapper"

        function App() {
        return (
            <CounterProvider>
            <Counter />
            <CounterList />
            </CounterProvider>
        );
        }

### 3. Utilizar o contexto para `salvar` dados

        function Counter() {
        const [count, setCount] = useState(0);
        const { saveCount } = React.useContext(CounterContext);

        return (
            <div>
            <h2>Contador: {count}</h2>
            <button onClick={() => setCount(count + 1)}>Incrementar</button>
            <button onClick={() => saveCount(count)}>Salvar</button>
            </div>
        );
        }

### 4. Utilizar o contexto para `ler` os dados

        function CounterList() {
        const { savedCounts } = React.useContext(CounterContext);

        return (
            <div>
            <h2>Valores Salvos</h2>
            <ul>
                {savedCounts.map((value, index) => (
                <li key={index}>{value}</li>
                ))}
            </ul>
            </div>
        );
        }

## React Hooks: Efeitos

No React, todos os componentes têm um **ciclo de vida (ou efeitos colaterais)**, que são os momentos em que eles: 

- ### Construído (mount)

    - Ocorre quando o componente aparece na tela pela primeira vez, podemos executar ações iniciais, como buscar dados de uma API ou adicionar eventos através do `addEventListener`.

- ### Atualizam (update)

    - Quando seu estado ou props mudam.

- ### Desmontam (unmount)

    - Quando saem da tela ou são removidos do DOM.

> Os ciclos de vida são fundamentais para entender quando e como o React deve atualizar um componente, executar efeitos colaterais, ou limpar recursos.

### Exemplos

- Manipular o DOM (exemplo: alterar o título da página).

- Atualizar estados quando uma propriedade for alterada.

- Fazer requisições HTTP (exemplo: buscar dados de uma API).

- Gerenciar timers (exemplo: `setTimeOut` ou `setInterval`).

- Subscrever eventos (exemplo: `addEventListener`).

- Lidar com WebSockets, LocalStorage e outras integrações externas.

- Atualizar estrutura de campos de formulário quando um outro campo for alterado.

### Como utilizar `useEffect`

O `useEffect` é um hook do React usado para lidar com efeitos colaterais em componentes funcionais. Por conta da sua escrita, ele parece difícil, mas é simples.

Essa função conta com **dois parâmetros obrigatórios**.

- ### Primeiro parâmetro: Função de callback

No primeiro parâmetro o `useEffect` recebe uma **função anônima** responsável por ser executada quando o efeito for ativado (callback), essa é a função do `mount` e `update`.

    React.useEffect(() => {
    // Código do efeito (executado quando necessário)
    });


 - ### Opcional: Função de retorno

 Ao retornar outra função anônima dentro do callback o componente a executa quando ele é destruído, essa é a função do `unmount`

    React.useEffect(() => {
    // Código do efeito (executado quando necessário)

    return () => {
        // Código de limpeza 
        // (executado antes de refazer o efeito ou desmontar)
    };
    });


- ### Casos de uso

    - Executar o `removeEventListener` para não acumular eventos sem o componente existir

    - Limpar intervalos de `setTimeOut` ou `setInterval`

    - Cancelar requisições em progresso com o `AbortController`

    - Desconectar de WebSockets ou Streams

---

- ### Segundo parâmetro: Lista de dependências

O segundo parâmetro do `useEffect` define **quando** o efeito deve ser executado. Obrigatoriamente deve ser uma lista (array) com ou sem elementos.

> ⚠️ Criar um novo efeito sem nenhuma dependência poderá causar loop infinito de renderização. Sempre passe uma dependência.

- ### Lista vazia - sem dependências 

    - Executa **somente uma vez**, quando o componente **monta**.

    - Útil para buscas iniciais de dados ou eventos globais.

            React.useEffect(() => {
            console.log("Executa apenas no mount!");
            }, []);
        
- ### `[dep1, dep2]`  Lista preenchida - com uma ou mais dependências

    - Executa quando qualquer uma das variáveis no array mudar.

    - Em quase todos os casos essas variáveis são props ou estados.

            const [count, setCount] = React.useState(0);
            const [name, setName] = React.useState("");

            React.useEffect(() => {
            console.log(`Count atualizado: ${count}`);
            }, [count]); // Executa quando 'count' mudar.

            React.useEffect(() => {
            console.log("Count ou Name mudou!");
            }, [count, name]); // Executa quando 'count' ou 'name' mudar.