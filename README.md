# SQL Arena

Plataforma de treino de SQL que roda inteira no navegador, no computador e no celular. Você escreve a consulta, vê a saída, e o app confere o resultado contra uma solução de referência.

## O que tem

- **Campanha**: 65 fases em 10 módulos, com conceito, missão, dica e solução.
  1. Fundamentos (SELECT, WHERE, ORDER BY, LIMIT, DISTINCT)
  2. Filtros avançados (IN, BETWEEN, LIKE, NULL)
  3. Agregações (COUNT, SUM, GROUP BY, HAVING)
  4. Junções (INNER, LEFT, anti-junção, auto-junção)
  5. Subconsultas (escalar, IN, EXISTS, correlacionada, tabela derivada)
  6. Funções e CASE (texto, datas, COALESCE, agregação condicional)
  7. Conjuntos e CTEs (UNION, INTERSECT, EXCEPT, WITH, recursão)
  8. Funções de janela (ROW_NUMBER, RANK, LAG, soma acumulada)
  9. DDL e DML (CREATE, INSERT, UPDATE, DELETE, VIEW, transação, índice)
  10. Chefões (problemas no estilo de entrevista)
- **Caça-bugs**: 9 consultas com defeitos clássicos (`= NULL`, `NOT IN` com NULL, LEFT JOIN anulado pelo WHERE, divisão inteira…).
- **Relâmpago**: 5 minutos para resolver o máximo de consultas sorteadas.
- **Simulado**: prova de 15 minutos com 3 questões exclusivas (fácil 20 pts, média 30, difícil 50), sorteadas de um banco de 12 que não aparece em outros modos. Correção só na entrega, com nota, gabarito e histórico.
- **Desafio do dia**: uma fase por dia, com bônus de XP e sequência.
- **Playground**: banco livre para qualquer comando.
- XP, 10 níveis (de Calouro a Lenda do SQL), estrelas por fase e progresso salvo no navegador.
- **Exportar progresso**: no Perfil, copie um código (ou baixe um .json) e importe em outro navegador ou aparelho.

## Como rodar

É um único arquivo, `index.html`. Abra no navegador ou sirva a pasta:

```bash
python -m http.server 8765
```

O motor é SQLite compilado para WebAssembly ([sql.js](https://github.com/sql-js/sql.js)), carregado de CDN na primeira abertura. Nenhum dado sai do navegador.

## Como a correção funciona

Cada execução recria o banco, roda o seu SQL e compara a saída com a da solução de referência: mesmo número de colunas e linhas, mesmos valores (tolerância de 0,006 em números) e, quando a fase pede, mesma ordem. Nomes de colunas não são conferidos. Nas fases de DDL/DML, o estado final do banco é que é comparado.

No console do navegador, `__selftest()` roda todas as soluções de referência e confirma que as consultas com bug são reprovadas.
