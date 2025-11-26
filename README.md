# **RELATÓRIO – Comparativo Técnico dos Métodos e Módulos da Aplicação**

## **1. Introdução**

A aplicação implementa quatro módulos principais de Computação Gráfica:

* **Curvas de Bézier**
* **Curvas B-Spline**
* **Superfície de Revolução (3D)**
* **Animação – Voo de Alus (trajetória Fibonacci)**

Cada módulo utiliza algoritmos matemáticos distintos, com níveis diferentes de suavidade, controle, realismo e intenção.

Este relatório apresenta uma **análise comparativa** entre os métodos, destacando:

* comportamento geométrico
* grau de controle do usuário
* usos típicos na área
* eficiência computacional
* qualidade visual
* robustez
* limitações

---

# **2. Comparativo entre Curvas de Bézier e B-Spline**

## **2.1. Tabela Comparativa Geral**

| Critério                        | Bézier                                            | B-Spline                                            |
| ------------------------------- | ------------------------------------------------- | --------------------------------------------------- |
| **Tipo de Controle**            | Global (todos os pontos afetam toda curva)        | Local (cada ponto influencia apenas parte da curva) |
| **Interatividade**              | Intuitiva, boa para aprender                      | Mais técnica, ideal para modelagem avançada         |
| **Complexidade Computacional**  | O(n²) pelo algoritmo de De Casteljau              | Maior, devido às bases Cox–de Boor                  |
| **Suavidade**                   | C⁰ (continuidade básica) ou C¹ se bem distribuída | C² naturalmente garantida                           |
| **Forma**                       | Sempre dentro do fecho convexo                    | Pode ultrapassar fecho convexo                      |
| **Sensibilidade a pontos**      | Muito alta                                        | Baixa (controle refinado)                           |
| **Aplicações típicas**          | Logos, tipografia, UI, formas simples             | CAD, modelagem 3D, superfícies NURBS                |
| **Facilidade de Implementação** | Alta                                              | Média/Alta                                          |
| **Suporte a pesos (racional)**  | Sim (implementado no app)                         | Não (no app atual)                                  |

---

## **2.2. Análise Comparativa Detalhada**

### **2.2.1. Suavidade e fluidez**

* **Bézier:**
  A suavidade depende da distribuição dos pontos. Maior quantidade gera curvas oscilantes.

* **B-Spline:**
  Suavidade C² garantida; ideal para geometria industrial.

❗ *Conclusão: B-Spline produz resultados mais suaves e estáveis.*

---

### **2.2.2. Controle do Usuário**

* **Bézier:**
  Alterar um único ponto altera a curva inteira.

* **B-Spline:**
  Movimento local → ideal para ajustes pontuais sem deformar toda a curva.

✔ *Vantagem da B-Spline em edição técnica e refinada.*

---

### **2.2.3. Estabilidade Numérica**

* Bézier de ordem alta tende a perder precisão.
* B-Spline lida melhor com muitos pontos, preservando estabilidade.

📌 *Em aplicações reais, quase sempre prefere-se B-Spline para curvas longas.*

---

# **3. Comparativo entre Curvas 2D e Superfície de Revolução 3D**

A seguir, compara-se o impacto das curvas quando usadas como perfil para gerar superfícies 3D.

## **3.1. Tabela Comparativa**

| Aspecto                     | Bézier como perfil            | B-Spline como perfil              |
| --------------------------- | ----------------------------- | --------------------------------- |
| **Manuseio do usuário**     | Desenho mais intuitivo        | Exige mais pontos para definição  |
| **Controle local**          | Não tem                       | Tem                               |
| **Risco de oscilação**      | Médio                         | Baixo                             |
| **Suavidade da superfície** | Boa, mas dependente dos pesos | Muito alta — ideal para modelagem |
| **Aplicação na indústria**  | Formas artísticas             | Produtos, peças mecânicas, NURBS  |

---

## **3.2. Impacto no Modelo 3D**

### **Com Bézier**

* Bom para formas orgânicas.
* Responde bem à manipulação manual.
* Sensível demais a pequenas mudanças → alterações bruscas na superfície.

### **Com B-Spline**

* Excelente para superfícies industriais.
* Gera uma malha uniforme, previsível e estável.
* Maior precisão geométrica.

💡 *Para superfícies realistas (vasos, peças, recipientes), B-Spline é a escolha ideal.*

---

# **4. Comparativo da Modelagem vs Animação (Voo de Alus)**

O módulo Alus utiliza outro tipo de spline: **Catmull–Rom**, escolhida por sua suavidade e caráter interpolador.

## **4.1. Comparação com Bézier e B-Spline**

| Critério              | Bézier     | B-Spline            | Catmull-Rom (Alus) |
| --------------------- | ---------- | ------------------- | ------------------ |
| **Interpola pontos?** | Sim        | Não necessariamente | Sim                |
| **Controle local**    | Não        | Sim                 | Sim                |
| **Uso típico**        | desenho 2D | CAD                 | animações          |
| **Suavidade**         | Média      | Alta                | Alta               |
| **Cálculo**           | Moderado   | Alto                | Baixo              |

---

## **4.2. Por que Catmull-Rom foi usado para o voo?**

* Interpola exatamente os pontos definidos pela trajetória Fibonacci.
* Suaviza a curva sem perder naturalidade.
* Muito rápido de computar para animação quadro a quadro.
* Ideal para caminhos animados (padrão em jogos e simuladores).

📌 *Para movimento suave e natural, Catmull-Rom supera Bézier e B-Spline.*

---

# **5. Comparativo Final – Síntese Geral**

## **5.1. Tabela Consolidada**

| Técnica                     | Suavidade             | Controle        | Eficiência | Uso Ideal                      |
| --------------------------- | --------------------- | --------------- | ---------- | ------------------------------ |
| **Bézier**                  | Média                 | Global          | Alta       | Formas simples, logos, arte    |
| **B-Spline**                | Muito alta            | Local           | Média      | Modelagem técnica, superfícies |
| **Catmull-Rom**             | Alta                  | Local interpola | Alta       | Caminhos animados              |
| **Superfície de Revolução** | Depende da curva base | Bom             | Média      | Objetos 3D simétricos          |

---

# **6. Conclusões**

1. **B-Spline é superior para modelagem precisa**, garantindo suavidade e controle local.
2. **Bézier é excelente para interfaces interativas**, mas limitado para curvas grandes.
3. **Superfície de Revolução produz melhor resultado quando o perfil é B-Spline**, devido à suavidade intrínseca.
4. **Catmull-Rom é a spline ideal para animações**, oferecendo suavidade e rapidez de cálculo.
5. A aplicação demonstra com clareza como **cada tipo de curva atende a propósitos diferentes**, permitindo comparar na prática suas características.
