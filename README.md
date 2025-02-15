# Ponderada de programação | Estrutura de Dados - HT e DHT

&ensp; Casos de teste são essenciais no contexto de uma DHT (Distributed Hash Table), pois garantem que a distribuição, armazenamento e recuperação de chaves funcionam corretamente. Como a estrutura distribui os dados entre diferentes nós de acordo com um critério específico (neste caso, o RA dos alunos), testar a correta inserção, busca e remoção de elementos assegura que a lógica de distribuição está alinhada com a expectativa do sistema. Além disso, como a DHT pode operar em ambientes dinâmicos, onde nós podem ser adicionados ou removidos, validar o comportamento sob diferentes cenários ajuda a prevenir falhas, como a perda de dados ou alocações incorretas. Testes bem estruturados também facilitam a depuração e a manutenção do código, reduzindo o risco de bugs e garantindo a confiabilidade do sistema ao longo do tempo.

# Casos de Teste para o Código da DHT

## Caso de Teste 1: Inserção de Alunos
**Pré-condição:**
- O sistema possui nós com IDs `{100, 500, 2000, 4000, 7000}`.
- Nenhum aluno foi inserido ainda.

**Etapas do Teste:**
1. Inserir os alunos:
   - Aluno 1: RA = 450, Nome = "Pedro"
   - Aluno 2: RA = 3500, Nome = "Maria"
   - Aluno 3: RA = 6200, Nome = "Lucas"
   - Aluno 4: RA = 400, Nome = "Joao"

**Pós-condição:**
- Verificar se os alunos foram inseridos nos nós corretos:
  - RA 450 deve estar no nó 500.
  - RA 3500 deve estar no nó 4000.
  - RA 6200 deve estar no nó 7000.
  - RA 400 deve estar no nó 500.

---

## Caso de Teste 2: Busca de Aluno Existente
**Pré-condição:**
- Os alunos já foram inseridos nos nós conforme o Caso de Teste 1.

**Etapas do Teste:**
1. Buscar o aluno com RA = 3500.

**Pós-condição:**
- O sistema deve retornar: "Aluno encontrado: Maria no nó 4000".

---

## Caso de Teste 3: Busca de Aluno Inexistente
**Pré-condição:**
- Os alunos já foram inseridos nos nós conforme o Caso de Teste 1.

**Etapas do Teste:**
1. Buscar o aluno com RA = 9999 (um RA que não existe).

**Pós-condição:**
- O sistema deve retornar: "Aluno não encontrado!".

---

## Caso de Teste 4: Remoção de Aluno Existente
**Pré-condição:**
- Os alunos já foram inseridos nos nós conforme o Caso de Teste 1.

**Etapas do Teste:**
1. Remover o aluno com RA = 450.

**Pós-condição:**
- O sistema deve retornar: "Aluno removido com sucesso".
- Verificar se o aluno com RA 450 não está mais no nó 500.

---

## Caso de Teste 5: Remoção de Aluno Inexistente
**Pré-condição:**
- Os alunos já foram inseridos nos nós conforme o Caso de Teste 1.

**Etapas do Teste:**
1. Remover o aluno com RA = 9999 (um RA que não existe).

**Pós-condição:**
- O sistema deve retornar: "Aluno não encontrado para remoção".

---

## Caso de Teste 6: Inserção de Aluno com RA Igual ao ID de um Nó
**Pré-condição:**
- O sistema possui nós com IDs `{100, 500, 2000, 4000, 7000}`.
- Nenhum aluno foi inserido ainda.

**Etapas do Teste:**
1. Inserir um aluno com RA = 500 (igual ao ID de um nó existente).

**Pós-condição:**
- Verificar se o aluno foi inserido no nó com ID 500.

---

## Caso de Teste 7: Inserção de Aluno com RA Menor que Todos os IDs dos Nós
**Pré-condição:**
- O sistema possui nós com IDs `{100, 500, 2000, 4000, 7000}`.
- Nenhum aluno foi inserido ainda.

**Etapas do Teste:**
1. Inserir um aluno com RA = 50 (menor que todos os IDs dos nós).

**Pós-condição:**
- Verificar se o aluno foi inserido no nó com ID 100 (o primeiro nó da lista).

---

## Caso de Teste 8: Inserção de Aluno com RA Maior que Todos os IDs dos Nós
**Pré-condição:**
- O sistema possui nós com IDs `{100, 500, 2000, 4000, 7000}`.
- Nenhum aluno foi inserido ainda.

**Etapas do Teste:**
1. Inserir um aluno com RA = 8000 (maior que todos os IDs dos nós).

**Pós-condição:**
- Verificar se o aluno foi inserido no nó com ID 100 (o primeiro nó da lista, devido ao comportamento circular da DHT).

---

## Caso de Teste 9: Busca de Aluno em um Nó Vazio
**Pré-condição:**
- O sistema possui nós com IDs `{100, 500, 2000, 4000, 7000}`.
- Nenhum aluno foi inserido no nó com ID 2000.

**Etapas do Teste:**
1. Buscar um aluno com RA = 1500 (que deveria estar no nó 2000, mas o nó está vazio).

**Pós-condição:**
- O sistema deve retornar: "Aluno não encontrado!".

---

## Caso de Teste 10: Remoção de Aluno em um Nó Vazio
**Pré-condição:**
- O sistema possui nós com IDs `{100, 500, 2000, 4000, 7000}`.
- Nenhum aluno foi inserido no nó com ID 4000.

**Etapas do Teste:**
1. Remover um aluno com RA = 3500 (que deveria estar no nó 4000, mas o nó está vazio).

**Pós-condição:**
- O sistema deve retornar: "Aluno não encontrado para remoção".

---

## Caso de Teste 11: Impressão do Estado dos Nós Após Remoção
**Pré-condição:**
- Os alunos já foram inseridos nos nós conforme o Caso de Teste 1.
- O aluno com RA = 450 foi removido conforme o Caso de Teste 4.

**Etapas do Teste:**
1. Executar a função `imprimirEstadoNos`.

**Pós-condição:**
- Verificar se o estado do nó 500 não contém mais o aluno com RA = 450.