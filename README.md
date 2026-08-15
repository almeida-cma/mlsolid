# 🧪 SOLID em Machine Learning

## Resumo Executivo

Este documento apresenta uma síntese do artigo **“Investigando o Impacto dos Princípios de Design SOLID na Compreensão de Código de Machine Learning”**, de Raphael Cabral, Hugo Villamizar, Marcos Kalinowski, Tatiana Escovedo, Maria Teresa Baldassarre e Hélio Lopes.

O estudo investigou, por meio de um experimento controlado com **100 cientistas de dados de 3 organizações**, se a aplicação dos cinco princípios SOLID poderia melhorar a compreensão de código de Machine Learning.

Os participantes analisaram duas versões de um sistema real de ML:

- uma versão original, desenvolvida sem a aplicação dos princípios SOLID;
- uma versão reestruturada utilizando SRP, OCP, LSP, ISP e DIP.

Os resultados apresentados no estudo indicam uma vantagem para o código estruturado com SOLID, especialmente em aspectos relacionados à compreensão, organização, extensão, substituição de componentes e redução de acoplamento.

### Principais resultados apresentados

| Princípio | Aspecto avaliado | p-valor | Cohen's d |
|---|---|---:|---:|
| **SRP** | Responsabilidades claras | 0.01 | 1.46 |
| **OCP** | Facilidade de extensão | 0.01 | 1.29 |
| **LSP + DIP** | Baixo acoplamento | 0.01 | 0.65 |
| **ISP** | Segregação de interfaces | 0.01 | 1.82 |
| **Geral** | Compreensão do código | 0.01 | 0.98 |

A principal mensagem do trabalho é que **Engenharia de Software deve fazer parte do desenvolvimento de sistemas de Machine Learning desde as etapas iniciais**, e não apenas quando o sistema chega à produção ou precisa ser mantido.

---

# 1. O problema: código de Machine Learning pode ser difícil de compreender

Projetos de Machine Learning envolvem experimentação constante. Cientistas de dados frequentemente precisam testar rapidamente:

- diferentes conjuntos de dados;
- técnicas de pré-processamento;
- algoritmos;
- modelos;
- métricas;
- parâmetros.

Essa dinâmica pode levar à concentração de várias responsabilidades em um mesmo código.

Uma forma simples de visualizar o problema é imaginar uma cozinha onde uma única pessoa faz tudo: compra os ingredientes, lava, corta, cozinha, serve e ainda lava a louça.

Em código de ML, uma situação semelhante pode ocorrer quando o mesmo bloco ou notebook concentra:

- carregamento de dados;
- pré-processamento;
- treinamento;
- avaliação;
- visualização.

### Consequências

- dificuldade para entender o que cada parte do código faz;
- dificuldade para modificar o sistema sem causar efeitos colaterais;
- dificuldade para reutilizar componentes;
- aumento da dívida técnica.

Outro fator importante é a diversidade da formação dos profissionais de dados. Muitos possuem formação em áreas como matemática, física ou economia e podem não ter recebido treinamento aprofundado em Engenharia de Software.

---

# 2. O experimento

## 2.1 Participantes

O experimento contou com **100 cientistas de dados**, distribuídos entre três organizações:

- **Universidade de Bari, Itália:** 32 estudantes;
- **PUC-Rio, Brasil:** 32 estudantes;
- **SERPRO, Brasil:** 36 profissionais.

## 2.2 Divisão dos grupos

Os participantes foram distribuídos em dois grupos:

| Grupo | Participantes |
|---|---:|
| **SOLID** | 48 |
| **Original** | 52 |
| **Total** | **100** |

## 2.3 Código analisado

Foi utilizado código real de um sistema relacionado a uma refinaria de petróleo.

O sistema tinha como objetivo prever a probabilidade de emissão de odores fortes.

O código original foi desenvolvido em Python utilizando Jupyter Notebooks e não aplicava os princípios SOLID.

Para o grupo experimental, a mesma funcionalidade foi reestruturada utilizando os cinco princípios SOLID.

---

# 3. Os cinco princípios SOLID

## 3.1 SRP — Single Responsibility Principle

### Responsabilidade Única

Cada classe ou componente deve possuir uma responsabilidade bem definida.

Em um sistema de ML, pode-se separar:

- geração ou carregamento de dados;
- divisão dos dados;
- treinamento;
- avaliação.

### Benefício

A separação facilita a compreensão e permite alterar uma responsabilidade sem necessariamente modificar as demais.

---

## 3.2 OCP — Open/Closed Principle

### Aberto para extensão, fechado para modificação

Um sistema deve permitir a inclusão de novos comportamentos sem exigir alterações extensas no código existente.

Por exemplo, novos modelos de Machine Learning podem ser adicionados por meio de novas classes que seguem uma abstração comum.

### Benefício

É possível ampliar o sistema sem modificar continuamente as funcionalidades já existentes.

---

## 3.3 LSP — Liskov Substitution Principle

### Substituição de Liskov

Uma implementação derivada deve poder substituir sua abstração ou classe-base sem quebrar o funcionamento esperado do sistema.

No contexto de ML, diferentes modelos podem seguir a mesma interface de treinamento e previsão.

### Benefício

O sistema pode trocar um modelo por outro sem exigir alterações importantes no componente que o utiliza.

---

## 3.4 ISP — Interface Segregation Principle

### Segregação de Interfaces

Interfaces devem ser específicas e não obrigar uma classe a implementar métodos que não fazem sentido para ela.

Por exemplo:

- uma interface para métricas de regressão;
- outra interface para métricas de classificação.

### Benefício

Cada componente implementa apenas as operações relevantes para seu contexto.

---

## 3.5 DIP — Dependency Inversion Principle

### Inversão de Dependência

Componentes devem depender de abstrações, e não diretamente de implementações concretas.

Por exemplo, um `Controller` pode depender da abstração `Model`, em vez de depender diretamente de `LinearModel` ou `RandomForestModel`.

### Benefício

O acoplamento é reduzido e os componentes podem ser substituídos com maior facilidade.

---

# 4. Entendendo as métricas estatísticas

## 4.1 p-valor

O p-valor é utilizado para avaliar a evidência contra a hipótese de que a diferença observada possa ser explicada pelo acaso.

No estudo, os resultados apresentados utilizam:

**p = 0.01**

Esse resultado indica uma diferença estatisticamente significativa segundo o critério adotado no estudo.

> Importante: p-valor não significa literalmente “99% de confiança de que a hipótese é verdadeira”. Ele representa a probabilidade de observar resultados tão extremos quanto os obtidos, assumindo a hipótese nula.

---

## 4.2 Cohen's d

O **Cohen's d** mede o tamanho do efeito, ou seja, o quanto os grupos diferem em termos padronizados.

Uma interpretação comum é:

- `d < 0.2` → efeito pequeno;
- `0.2 ≤ d < 0.5` → efeito pequeno a moderado;
- `0.5 ≤ d < 0.8` → efeito moderado a grande;
- `d ≥ 0.8` → efeito grande.

No estudo:

- **ISP:** d = 1.82;
- **SRP:** d = 1.46;
- **OCP:** d = 1.29;
- **LSP + DIP:** d = 0.65;
- **Geral:** d = 0.98.

O maior efeito apresentado foi observado para **ISP**, com `d = 1.82`.

---

# 5. Demonstração prática

Uma forma didática de compreender os princípios é comparar um código de ML em que todas as responsabilidades estão misturadas com uma versão estruturada.

## Código sem SOLID

Um único bloco pode:

1. gerar os dados;
2. dividir treino e teste;
3. criar o modelo;
4. treinar;
5. realizar previsões;
6. calcular métricas.

Embora possa funcionar corretamente, esse formato concentra muitas responsabilidades.

## Código com SRP

As responsabilidades podem ser separadas em componentes como:

```text
DataGenerator
      ↓
DataSplitter
      ↓
ModelTrainer
      ↓
ModelEvaluator
```

O resultado numérico pode permanecer o mesmo, mas a organização do código melhora.

---

# 6. OCP na prática

Com uma abstração comum:

```text
             Model
               │
       ┌───────┴────────┐
       ↓                ↓
LinearModel      RandomForestModel
```

O sistema pode trabalhar com diferentes modelos sem precisar modificar a lógica central.

A principal vantagem está na extensão do sistema.

---

# 7. LSP + DIP na prática

Um `Controller` pode receber qualquer objeto que respeite a abstração `Model`:

```text
Controller
    │
    ↓
  Model
  /    ↓     ↓
Linear  RandomForest
```

Assim, o controlador não precisa conhecer detalhes das implementações concretas.

Isso reduz o acoplamento e facilita a substituição de modelos.

---

# 8. ISP na prática

As interfaces podem ser separadas de acordo com o tipo de problema:

```text
RegressionEvaluator
    ├── MSE
    └── R²

ClassificationEvaluator
    ├── Acurácia
    └── F1
```

Dessa forma, cada avaliador implementa apenas as operações que fazem sentido para seu tipo de problema.

---

# 9. Resultados do experimento

O material apresenta a seguinte comparação de compreensão percebida:

| Versão do código | Média |
|---|---:|
| Código original | **3.1** |
| Código com SOLID | **4.2** |

Isso corresponde a uma melhoria apresentada de aproximadamente **35% na compreensão percebida**.

## Resultados estatísticos

| Princípio | Pergunta avaliada | p-valor | Efeito (d) | Significativo? |
|---|---|---:|---:|---|
| **SRP** | Responsabilidades claras | 0.01 | 1.46 | ✅ Sim |
| **OCP** | Facilidade de extensão | 0.01 | 1.29 | ✅ Sim |
| **LSP + DIP** | Baixo acoplamento | 0.01 | 0.65 | ✅ Sim |
| **ISP** | Segregação de interfaces | 0.01 | 1.82 | ✅ Sim |
| **Geral** | Compreensão do código | 0.01 | 0.98 | ✅ Sim |

---

# 10. Implicações práticas

## Para cientistas de dados

Conhecer princípios de Engenharia de Software pode ajudar a produzir código:

- mais organizado;
- mais fácil de compreender;
- mais fácil de modificar;
- mais reutilizável;
- mais adequado ao trabalho em equipe.

## Para empresas

Código mais estruturado pode contribuir para:

- redução da dívida técnica;
- manutenção mais simples;
- evolução dos sistemas;
- inclusão de novos modelos;
- maior facilidade de colaboração entre profissionais.

## Para educadores

A formação em Ciência de Dados pode se beneficiar da inclusão de conteúdos de Engenharia de Software, incluindo:

- princípios SOLID;
- orientação a objetos;
- modularização;
- abstração;
- baixo acoplamento;
- refatoração;
- testes;
- manutenção de software.

---

# 11. Limitações

Os resultados devem ser interpretados considerando as limitações do estudo.

Entre elas:

- amostra composta por participantes de organizações específicas;
- concentração significativa de participantes com formação em Computação;
- utilização de um código-base específico;
- necessidade de replicação do experimento em outros contextos.

Portanto, os resultados fornecem **evidência favorável** ao uso de SOLID em código de ML, mas não devem ser interpretados como prova definitiva de que os princípios produzirão os mesmos efeitos em todos os projetos e equipes.

---

# 12. Conclusão

O estudo mostra que princípios tradicionais de Engenharia de Software podem ser relevantes para sistemas de Machine Learning.

A aplicação de SOLID pode contribuir para:

- melhorar a compreensão do código;
- separar responsabilidades;
- facilitar extensões;
- permitir substituição de modelos;
- reduzir acoplamento;
- organizar interfaces;
- facilitar manutenção.

A principal conclusão é que **Machine Learning não envolve apenas dados e modelos: também envolve software**.

Consequentemente, práticas de Engenharia de Software devem fazer parte do desenvolvimento de sistemas de ML desde as primeiras etapas do projeto.

---

## 📚 Referência

**CABRAL, Raphael; VILLAMIZAR, Hugo; KALINOWSKI, Marcos; ESCOVEDO, Tatiana; BALDASSARRE, Maria Teresa; LOPES, Hélio.**

*Investigando o Impacto dos Princípios de Design SOLID na Compreensão de Código de Machine Learning.*

CAIN 2024.

DOI: `10.1145/3644815.3644957`

---

### 👨‍🏫 Material didático

**Cristiano Almeida**  
Disciplina: **Engenharia de Software**

Material baseado no artigo original.
