# Eventos

## Diferenças entre eventos no React e Vanilla JavaScript

- No React os eventos são **encapsulados** em um sistema chamado SyntheticEvent, que melhora o desempenho e a compatibilidade entre navegadores.  

- No HTML faríamos algo como `<button onclick="handleClick()">`, já nos componentes passamos uma função diretamente: `<button onClick={handleClick}>`.

- No React, a função de evento recebe automaticamente um **objeto do evento**, que pode ser utilizado como referência ao DOM.

## Escrita Vanilla JS x React

|                  Vanilla JS                 | React       |
|:-------------------------------------------:|-------------|
| `onclick / addEventListener('click')`       | `onClick`   |
| `onchange  /  addEventListener('change')`   | `onChange ` |
| `onkeydown  /  addEventListener('keydown')` | `onKeyDown` |
| `onsubmit  /  addEventListener('submit')`   | `onSubmit`  |


## SyntheticEvent

- É um **wrapper(encapsulador)** sobre os eventos nativos do navegador no React.

- Ele serve para garantir que os eventos funcionem de forma **consistente** em diferente navegadores e para melhorar a **eficiência da perfomance**.

- O React gerencia todos os eventos através de um **event delegation** em um único listener no nivel superior.

- Ele sabe quais eventos criar ou destruir conforme faz a renderização dos componentes em tela.

> Isso melhora a performance porque evita a criação de múltiplos event listeners no DOM.

## Quando usar addEventListener

Pode utilizar em casos onde você não tem acesso direto aos componentes, por exemplo o `body`.

- Caso queira utilizar `keydown` para adicionar teclas de atalho apenas quando um componente existir você pode utilizar o `addEventListener`.
