# Componentes

Um componente React é com se fosse uma tag HTML personalizada do seu próprio jeito, da forma como quiser.

- **Bloco de UI:** Como se fosse uma peça de lego, porém feita de código que representa uma parte da interface de usuário.

- **Tags customizadas:** Um componente abre e fecha uma tag, e essas tags **OBRIGATÓRIAMENTE** precisam começar com a **primeira letra** maiúscula.

- **Funcional:** Precisa estar dentro de uma função onde o HTML a ser desenhado na página será retornado, é **obrigatório** o retorno, sendo o **HTML**, **nulo** ou um **Fragmento**

- **Reutilizável:** Pode ser reutilizado em diferentes partes da aplicação.

- **Recebe estilização:** Recebe estilos CSS através das propriedades `style` (objetos) ou `className` (mesma coisa que o class do HTML).

- **Multi-definições:** Pode ser atômico onde não há muita lógica funcional, ou com mais inteligência integrado nele, pode ter muita ou pouca lógica integrada.

## Estrutura básica

- Obrigatório ser uma **função** (qualquer tipo de função, arrow function, function e etc.)

- Obrigatório **começar com letra maiúscula.**

- Obrigatório retornar um **HTML** ou **null**

        const MeuComponente = () => {
            return (
                <button>Botão</button>
            )
        };