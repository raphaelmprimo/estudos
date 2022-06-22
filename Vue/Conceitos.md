# Conceitos do Vue

## Single-File Components
Aquivo `.vue` que é considerado um pedaço da aplicação que pode ter as seguintes estruturas:

- Template - **obrigatório**
- Script
- Style

### Estrutura
```html
<template>
    <h1>Hello World</h1>
</tamplate>
<script>
export default {
    
}
</script>
<style>
h1 {
    color: blue;
}
</style>
```

## Data-binding
Conexão de dados entre o Model do JS com a View (DOM)

### Tipos

#### One-way binding
Conexão de mão única do Model do JS com a View (DOM). Ao renderizar a página o JS envia para a View os dados dessa binding. Alterando os dados do Model, a view é atualizada.

#### Two-way binding (Utilizada pelo Vue)
Há a conexão tanto do Model do JS com a View (DOM) - semelhante ao One-Way binding - quanto o contrário, a View com o Model do JS. Desta forma ao realizar uma alteração de dados tanto no Model quanto na View, ambos sofrem atualização.

### Exemplos
```html
<template>
    <h1>Hello {{ name }}</h1>
    <input type="text" v-model="name">
</tamplate>
<script>
export default {
    data: () => ({
        name: 'Raphael'
    })
}
</script>
```
É utilizado a propriedade `data` para definir os dados que vão estar conectados através do **Two-way binding**. No exemplo acima foi definido a propriedade `name` e colocado valor inicial `Raphael`.

Para evidenciar a **Two-way binding**, foi colocado um input de texto usando a diretiva `v-model` que recebe o nome da propriedade a vincular, no caso `name`

```html
<template>
    <h1 v-bind:style="decoration">Hello {{ name }}</h1>
    <input type="text" v-model="name">
</tamplate>
<script>
export default {
    data: () => ({
        name: 'Raphael',
        decoration: 'text-decoration:underline'
    })
}
</script>
```

É possível também passar parâmetros para elementos do HTML usufruindo do **Two-way binding**. No exemplo acima, ao colocar um `style in-line` foi prefixado com `v-bind:`, desta forma o conteúdo do parâmetro passa a ser uma propriedade do Model, não mais uma string.

Outra forma de fazer isso é prefixar somente com `:`, como mostra abaixo:
```html
<h1 :style="decoration">Hello {{ name }}</h1>
```

## Diretivas

### v-model
Faz o bind do valor de uma propriedade com o elemento do template

#### Exemplo

```html
<template>
    <h1>Hello {{ name }}</h1>
    <input type="text" v-model="name">
</tamplate>
<script>
export default {
    data: () => ({
        name: 'Raphael'
    })
}
</script>
```

### v-bind
Faz 

### v-for
Utilizada para fazer uma iteração dentro de uma propriedade, repetindo o elemento do `template` em cada iteração. Esta diretiva depende de passar um `bind` para uma `key` para cada item da iteração: `:key=""`

#### Estrutura
Pegar os dados de cada item dentro de uma iteração:
```html
<li v-for="task in tasks"></li>
```

Pegar os dados de cada item com sua posição na iteração (index):
```html
<li v-for="(task, index) in tasks" :key="`${task}-${index}`"></li>
```

#### Exemplo

```html
<template>
    <div>
        <h1>Lista de Tarefas</h1>
        <ul>
            <li
            v-for="task in tasks"
            :key="`${task}-${index}`"
            >
                {{ task.name }}
            </li>
        </ul>
    </div>
</tamplate>
<script>
export default {
    data: () => ({
        tasks: [
            {
                name: 'Estudar Vue.js',
                isDone: false
            }
        ]
    })
}
</script>
```

### v-if e v-else
Diretivas condicionais para a exibição de um elemento no template.

#### Exemplo
```html
<template>
    <h1 v-if="showName">Hello {{ name }}!</h1>
    <h1 v-else="showName">Hello World!</h1>
</tamplate>
<script>
export default {
    data: () => ({
        name: 'Raphael',
        showName: false
    })
}
</script>
```

### Diretivas personalizadas
É possível criar as suas próprias diretivas

#### Exemplo
```html
<template>
    <h1 v-bind:style="decoration">Hello {{ name }}</h1>
    <input type="text" v-model="name" v-focus>
</tamplate>
<script>
const focus = {
    inserted: (element) => {
        element.focus()
    }
}
export default {
    directive: {
        focus
    }
    data: () => ({
        name: 'Raphael',
        decoration: 'text-decoration:underline'
    })
}
</script>
```

## Eventos e Métodos
> **Note**: para acessar o `this` para acessar as propriedades dentro dos métodos

### @click ou v-on:click

#### Exemplo
```html
<template>
    <div>
        <h1>Lista de Tarefas</h1>
        <ul>
            <li
                v-for="task in tasks"
                :key="`${task}-${index}`"
            >
                {{ task.name }}
                <button
                    @click="remove(task)"
                >
                    &times;
                </button>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    data: () => ({
        tasks: [
            {
                name: 'Estudar Vue.js',
                isDone: false
            }
        ]
    }),
    methods: {
        remove (task) {
            this.tasks = this.tasks.filter(task => t.name !== task.name);
        }
    }
}
</script>
```

### @dblclick
Duplo clique

### @keyup
Pressionar e soltar a tecla.

Pode ser passado um modificador da tecla que deseja adicionar o evento: `@keyup.enter`