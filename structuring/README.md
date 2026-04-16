# Fundamentos 

React é uma biblioteca para construir interfaces, e toda interface é composta por três pilares principais:

- HTML -> Define a estrutura da página(Esqueleto).      

- CSS -> Estilização e aparência visual.   

- JavaScript -> Interatividade e automação.      
 
> ### ⚠️ O React não substitui essas tecnologias, ele apenas organiza dentro de componentes reutilizáveis e processa de forma mais inteligente, ele não cria algo novo, apenas otimiza o que já existe.   

## JSX (JavaScript XML)

- Sintaxe que permite escrever código HTML dentro do JavaScript.   

- Dentro do React, facilita a criação de interfaces via componentes, tornando o código mais intuitivo.    

- Não precisa criar vários arquivos para ter um componente visual.    

---    

**Por exemplo**, em vez de escrever o componente com puro JavaScript como: 

`return React.createElement("h1", null, "Hello world!");`

Se pode escrever como se fosse HTML padrão: 

`return <h1>Hello world!</h1>;`

O React sozinho compila(converte) JSX para `React.createElement()`, então escrever as tags em HTML é apenas "sugar sintax" para criar elementos de forma mais legível.

> ### ⚠️ Em alguns momentos você pode ver a extensão `.jsx` no arquivo de componentes, mas ela nem sempre é necessária.

## Fragmentos

No JSX, a parte escrita do HTML **sempre precisa retornar um único elemento pai.**

- Pode ser qualquer elemento HTML, como uma `div` ou qualquer outro.   
- Pode ser uma tag vazia, que é conhecida como `Fragmento`, ele permite agrupar sem criar elementos adicionais.

### 🚫 **Não funciona!**

Retornar elementos **soltos**, é necessário um elemento **pai** para agrupar:

    return (
        <h1> Hello world! </h1>
        <p> Welcome! </p>
    );

### ✅ **Funciona!**

- ### Usar `div`(Gera um nó extra no DOM)

        return (
            <div>
                <h1> Hello world! </h1>
                <p> Welcome! </p>
            </div>
        );

- ### Usar tag vazia `<>`(Não gera nada a mais no DOM)

        return (
            <>
                <h1> Hello world! </h1>
                <p> Welcome! </p>
            </>
        );

    Ou(Sinônimo): 

        return (
            <React.Fragment>
                <h1> Hello world! </h1>
                <p> Welcome! </p>
            </React.Fragment>
        );
    
    > ### ⚠️ Retonar dois ou mais elementos soltos, sem um "Wrapper" resultará em erros de compilação.

## Como o código é convertido(BabelJS)

O Babel é um "transpilador" de JavaScript, ele é um conversor, converte algo em outra.

**Exemplo -**

Ele pega código moderno (ES6+) e converte para uma versão compatível com a maioria dos navegadores.

    // Significa que se você escrever algo como:
      const soma = (a, b) => a + b;

    // O babel vai converter isso em:
      function soma(a, b) {
        return a + b;
      }

## Como estilizar o HTML dentro do React

### CSS interno (inline)

- Escrever como **objeto** e não como string(usado no CSS padrão).

- As propriedades do CSS são passadas em **camelCase**.

`app.js`

    export default function App() {
        return (
           <div style={{ backgroundColor: "lightblue", padding: "20px" }}>
           Background azul
           </div>
        );
    }

### CSS externo

- CSS comum

- Importar dentro do componente React

`styles.css`

    .container {
        background-color: lightblue;
        padding: 20px;
    }

`app.js`

    import "./styles.css";
    
    function App() {
      return <div className="container">Background Azul</div>;
    }

### CSS modules

 - Cria classes que viram variáveis do JS para manipulação em React

`styles.module.css`

    .container {
        background-color: lightblue;
        padding: 20px;
    }

`app.js`

    import styles from "./styles.module.css";

    export default function App() {
        return <div className={styles.container}>Background Azul</div>;
    }

### CSS-in-JS

- Escrever CSS inteiramente no JS com ajuda de bibliotecas

`app.js`

    import styled from "styled-components";

    const Container = styled.div`
        background-color: lightblue;
        padding: 20px;
    `;

    export default function App() {
        return <Container>Background Azul</Container>;
    }

### Sass e outros pré-processadores

- Mesma lógica do CSS externo e CSS modules

`styles.scss`

    $bg-color: lightblue;

    .container {
        background-color: $bg-color;
        padding: 20px;
    }

`app.js`

    import "./styles.scss";

    export default function App() {
        return <div className="container">Background Azul</div>;
    }

### TailwindCSS e outras bibliotecas

- Utilização de classes prontas

`app.js`

    export default function App() {
        return <div className="bg-blue-300 p-5">Background Azul</div>;
    }

> Cada uma com pontos positivos e negativos, cabe escolher qual a melhor devido ao contexto do projeto.