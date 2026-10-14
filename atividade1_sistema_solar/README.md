# Atividade 1 – Mini Sistema Solar

**Disciplina:** Computação Gráfica
**Atividade:** Mini Sistema Solar (Transformações geométricas)
**Integrantes:**
- Angelo Ricardo de Souza Teixeira
- Hamilton Ferreira de Souza 

## Descrição
A solução usa apenas `make_translation`, `make_rotation_z` e `make_scale`, combinadas com `@`:

- **Sol:** `R(anguloSol) @ S(0.25)`, que gira em torno do próprio centro.
- **Planeta:** `R(anguloOrbita) @ T(0.6) @ R(anguloRotacaoPlaneta) @ S(0.1)`, que orbita o Sol com raio 0.6 e gira no próprio eixo com velocidade diferente.
- **Lua:** reaproveita a órbita do planeta (`R(anguloOrbita) @ T(0.6)`) e acrescenta `R(anguloOrbitaLua) @ T(0.2) @ S(0.05)`, orbitando o planeta com raio 0.2 e acompanhando seu movimento.
- **Teclado:** ↑ e ↓ alteram `velocidadeOrbita` (proporcional a `deltaTime`), limitada com `max(0, ...)` para nunca ficar negativa.

A escala fica sempre à direita de tudo, para não alterar os raios das órbitas.

![Resultado](capturas/resultado.png)

## Resposta da questão
**Por que a órbita utiliza `R @ T` e a rotação própria do planeta fica à direita da translação?**

Em uma expressão `A @ B @ ponto`, a matriz mais à direita é aplicada primeiro. Na órbita (`R @ T`), o planeta é primeiro transladado para a distância 0.6 e depois a rotação `R` é aplicada em torno da origem, onde está o Sol. Assim, o planeta descreve um círculo ao redor do Sol. Na ordem inversa (`T @ R`), o planeta apenas giraria no próprio lugar e depois seria deslocado, sem orbitar.

A rotação própria precisa ser aplicada enquanto o planeta ainda está na origem, para girar em torno do seu próprio centro. Por isso ela fica à direita da translação: `R_orbita @ T(0.6) @ R_propria @ S`. Se ela ficasse à esquerda de `T`, também giraria o planeta em torno do Sol, virando uma segunda órbita em vez de uma rotação no próprio eixo.
