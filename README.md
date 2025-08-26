# Lista Linear (Sequencial) — **Exclusão de Elemento**

> Disciplina: Estrutura de Dados (C++)  
> Tema: Lista linear implementada com **array estático** (`int lista[MAX]` + `int nElementos`)  
> Objetivo: Implementar a função **`excluirElemento()`** utilizando a função **`posicaoElemento()`** para evitar duplicação de código. 

---

## 1) Contexto e Modelo de Dados

Nesta atividade, trabalharemos com uma **lista linear sequencial** (também chamada de *lista estática*), armazenada em um **array** de tamanho fixo `MAX` e controlada pela variável `nElementos`:

- `lista[MAX]`: armazena os valores inteiros;
- `nElementos`: quantidade atual de itens válidos (elementos ocupando as posições `0 ... nElementos-1`);
- O menu já dispõe de opções para **inserir**, **buscar**, **exibir** e **excluir**.

**Importante**:
1. Os elementos válidos estão sempre nas posições `0` até `nElementos - 1`.
2. Não deve haver "buracos" entre elementos — ao remover um item, **deslocamos** os seguintes uma posição à esquerda.
3. Nunca acessar índices `>= nElementos` (evita *lixo* ou leitura fora do limite).

---

## 2) Revisão conceitual (Arrays em C++)

- **Array estático**: tamanho definido em tempo de compilação (ex.: `const int MAX = 10; int lista[MAX]{};`).  
- **Acesso por índice**: `lista[i]` é **O(1)** (tempo constante).  
- **Inserção no fim**: se houver espaço, fazer `lista[nElementos] = valor; nElementos++` (**O(1)**).  
- **Busca linear**: varrer do índice `0` até `nElementos-1` comparando valores (**O(n)**).  
- **Exclusão**: localizar a posição **p** e deslocar os itens das posições `p+1 ... nElementos-1` para a esquerda (**O(n)**).

> Dica para o menu: `system("cls")` e `system("pause")` existem no Windows. Em outras plataformas, você pode comentar/remover essas linhas.

---

## 3) Evitando duplicação com `posicaoElemento(int valor)`

A busca por um valor aparece em vários pontos do programa (ex.: **buscar** e **excluir**). Para **não duplicar código**, utilizamos uma **função utilitária** que centraliza a busca:

### 3.1) Assinatura (já fornecida no projeto)
```cpp
int posicaoElemento(int valor);
```

### 3.2) Responsabilidade
- Percorrer as posições válidas (`0` a `nElementos-1`) da lista;
- **Retornar o índice** da **primeira ocorrência** do valor buscado;
- **Retornar `-1`** caso o valor **não** esteja presente na lista.

> **Por que retornar a primeira ocorrência?**  
> Mantém a função previsível e facilita operações como exclusão (remove o primeiro que encontrar).


---

## 4) Implementando `excluirElemento()`

- **Ler do usuário** o número a ser excluído;
- **Buscar** o número na lista usando **`posicaoElemento(valor)`**;
- **Se encontrado**: remover deslocando os elementos à esquerda; **decrementar `nElementos`**;
- **Se não encontrado**: exibir a mensagem **`"elemento não encontrado"`** 


---

## 5) Interações com o menu

- A função `excluirElemento()` deve ser chamada pela opção **6 – Excluir elemento** do menu.  
- A função `buscarElemento()` (opção 4) também deve usar **`posicaoElemento()`** — evite repetir um laço de busca ali.

Exemplo de uso dentro de `buscarElemento()` (já compatível com o projeto):
```cpp
void buscarElemento() {
    int valor;
    cout << "Digite o elemento que queira buscar: ";
    cin >> valor;

    int pos = posicaoElemento(valor);

    if (pos != -1) {
        cout << "O elemento foi encontrado na posicao " << pos << endl;
    } else {
        cout << "O elemento digitado nao foi encontrado" << endl;
    }
}
```

---

## 6) Casos de teste sugeridos

1. **Excluir em lista vazia**: opção 6 sem inserir nada → deve avisar que está vazia.  
2. **Excluir elemento inexistente**: insira `[3, 7, 9]`, tente excluir `5` → `"elemento nao encontrado"`.  
3. **Excluir primeiro elemento**: de `[3, 7, 9]` exclua `3` → resultado `[7, 9]`, `nElementos = 2`.  
4. **Excluir último elemento**: de `[7, 9]` exclua `9` → resultado `[7]`, `nElementos = 1`.  
5. **Excluir elemento do meio**: de `[2, 5, 8, 10]` exclua `8` → resultado `[2, 5, 10]`, `nElementos = 3`.  
6. **Inserir duplicados (se permitido)**: se decidir permitir duplicados, exclua `5` em `[5, 5, 5]` → deve restar `[5, 5]`.  
   - *Observação*: o código acima remove **apenas a primeira ocorrência**. Para remover **todas**, repita exclusões enquanto `posicaoElemento(valor) != -1`.

---

## 7) Análise de complexidade

- **Busca (`posicaoElemento`)**: `O(n)` no pior caso (precisa varrer a lista inteira).  
- **Exclusão**: `O(n)` devido ao deslocamento após a posição removida.  
- **Espaço adicional**: `O(1)` — operação feita *in place* no array.

> Em listas **encadeadas**, a exclusão pode ser feita sem deslocamento, mas a busca continua `O(n)` se a lista não for ordenada.

---


## 8) Checklist para entrega

- [ ] `excluirElemento()` implementada conforme especificação.  
- [ ] `posicaoElemento()` retorna **a primeira ocorrência** e é **utilizada** por `excluirElemento()` e `buscarElemento()`.  
- [ ] Mensagens de saída conforme exemplos (atenção à ortografia simples sem acentos, se preferir manter padrão do projeto).  
- [ ] Testes executados (incluindo casos de sucesso e erro).  
- [ ] Código comentado explicando as decisões principais.

---

Boa prática e bons estudos! ✨

