# Propriedades (props)

Uma propriedade é como se fosse um atributo do HTML, porém customizado por você, como uma peça de lego que têm várias cores, tamanhos e formas diferentes.

- **Personalização dinâmica:** as propriedades (ou props) permitem modificar o comportamento e a aparência do componente de forma flexível.    

- **Atributos customizados:** funcionam como atributos HTML, mas são passadas para componentes React como atributos desse componente, juntamente com os atributos HTML.   

- **Passagem de dados:** um componente pode receber valores externos como texto, números, objetos, funções ou até mesmo outros componentes através das props.    

- **Imutabilidade:** as propriedades são somente leitura dentro do componente, ou seja, não podem ser modificadas diretamente.

- **Padrões opcionais:** um componente pode definir valores padrão para as propriedades caso nenhuma seja fornecida.

- **Composição:** elas podem ser usadas para renderizar outros componentes dentro do componente pai, tornando-o mais flexível. 

- **Propriedades especiais:** `children` e `key` são duas propriedades do React e não podem ser utilizadas de maneira customizada.  

    - **`Children:`** é uma prop especial do React que representa o conteúdo passado entre as tags do componente.

    - **`Key:`** é uma prop usada pelo React para identificar elementos de uma lista e otimizar a renderização.

## Observações

- Valores dinâmicos como children, variant e as props devem estar entre {}.    

- Para definir valores padrões utilizamos da seguinte maneira: `variant = "nome"`.

- Para pegar propriedades do HTML podemos utilizar `...props` e adicionar antes de fechar a tag `>`

## Exemplo

          function Button({ children, variant }) {
            return (
              <button
                className={variant === "primary" ? "bg-purple-500" : "bg-gray-500"}
              >
                {children}
              </button>
            );
          }

          function App() {
            return <Button variant="primary">Meu Botão</Button>;
          }