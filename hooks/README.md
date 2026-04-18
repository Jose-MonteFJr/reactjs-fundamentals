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

## prevValue

Utilizado para validação com estado anterior ou para incrementação.

- Em uma atualização é possível utilizar o valor anterior do estado.

- Se o novo valor depender do estado anterior, passe uma função anónima que tem como primeiro parâmetro o prevValue.