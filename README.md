# Predição de qualidade de produtos da indústria de refino de petróleo

#### Aluno: [André Seichi Ribeiro Kuramoto](https://github.com/andrekuramoto).
#### Orientadora: [Manoela Kohler](https://github.com/manoelakohler).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

---

### Resumo

Refinarias de petróleo, por meio de processos físicos de separação e reações, geram produtos (derivados de petróleo) para comercialização no mercado. Tais produtos devem atender requisitos de qualidade mínimos especificados pela ANP ([Agência Nacional de Petróleo](https://www.gov.br/anp)). A qualidade dos derivados é controlada por meio de ajustes operacionais da planta de processamento de petróleo. 

Produzir derivados com qualidade superior à especificada podem gerar perdas econômicas tais como: utilizar frações mais nobres do petróleo em produtos de menor valor agregado, maior consumo de insumos e perdas de energia. Portanto, para se atender à especificação e obter eficiência em produção de derivados, é necessário medir e controlar a qualidades dos produtos.

Devido a variações das características do petróleo, dos insumos, dos equipamentos da planta de processamento e do meio ambiente, fazem-se necessários ajustes nos parâmetros da planta de produção para se manterem controladas as qualidades dos derivados.

A qualidade dos produtos é medida por ensaios laboratoriais realizados a partir de amostras da produção. Para se monitorar e controlar a qualidade durante o período entre momentos de amostragem e ensaios laboratoriais a literatura [[1]](https://www.sciencedirect.com/science/article/abs/pii/S0098135421001022) propõe o uso de modelos matemáticos empíricos ou fenomenológicos que estimam a qualidade a partir de variáveis simples de serem medidas no processo produtivo como densidades, pressões, temperaturas e vazões. Essas variáveis são medidas em taxas muito mais altas (da ordem de minutos) que a taxa de amostragem e ensaio laboratorial dos produtos (da ordem de horas). Sabe-se que a qualidade de um produto possui dependência temporal com as variáveis de processo, ou seja, a qualidade medida de uma amostra da produção tem correlação com as variáveis simples observadas no passado no processo produtivo. 

Neste trabalho, propõe-se utilizar aprendizado profundo (*Deep Learning*, DL) para estimar a qualidade atual (corrente) de um derivado a partir do histórico de variáveis do processo produtivo e de medições passadas da qualidade. Deseja-se atualizar a estimativa da qualidade em taxa compatível com as taxas de medição das variáveis simples do processo, ou seja, em taxa muito superior à taxa de medição laboratorial de qualidade.

Modelo foram desenvolvidos utilizando o framework [TensorFlow](https://www.tensorflow.org/) em código [Python](https://www.python.org/). Foram ensaiados modelos lineares, redes neurais densas (*Dense Neural Networks*, DNN), redes neurais convolucionais (*Convolutional Neural Networks*, CNN) e redes neurais recorrentes (*recurrent neural networks*, RNN) do tipo LSTM (*long short-term memory*)[[2]](https://www.bioinf.jku.at/publications/older/2604.pdf).

O principal desafio abordado aqui é a disponibilidade do *label* em taxa muito inferior às demais variáveis de entrada do modelo e à própria taxa de atualização do modelo.

Para viabilizar o treinamento, validação e testes do modelo, foram criadas uma função objetivo (*loss function*) e uma função de cáculo de métrica de validação que consideram a diferença de taxa existente entre o *label* e demais variáveis do modelo. Essas funções especiais criadas computam o objetivo e a métrica de validação apenas para os instantes em que o *label* está disponível. Os demais instantes (dos *labels* faltantes) não influenciam nem o resultado da função objetivo nem a métrica de validação, ou seja, não influenciam o cálculo de ajuste de pesos da rede. Dessa forma, evita-se aproximar os valores faltantes do *label*, por exemplo por interpolação, o que não é adequado devido ao longo período de dados faltantes (ordem de horas) em relação às demais variáveis do processo (ordem de minutos).

Os resultados mostram a viabilidade dessa abordagem de funções especiais para cálculo de objetivo de métricas de validação quando não se tem disponível o *label* em taxa compatível com as demais variáveis.

#### Referências

[[1]](https://www.sciencedirect.com/science/article/abs/pii/S0098135421001022) Daniela C.M. de Souza, Luís Cabrita, Cláudia F. Galinha, Tiago J. Rato, Marco S. Reis, "A Spectral AutoML approach for industrial soft sensor development: Validation in an oil refinery plant", Computers & Chemical Engineering, Volume 150, 2021.

[[2]](https://www.bioinf.jku.at/publications/older/2604.pdf) Sepp Hochreiter, Jürgen Schmidhuber, "Long Short-Term Memory", Neural Computation 9(8):1735-1780, 1997.

### Abstract 

Oil refineries, through physical separation and reaction processes, generate products (oil derivatives) for commercialization in the market. Such products must meet minimum quality requirements specified by the ANP ([Agência Nacional de Petróleo](https://www.gov.br/anp)). The quality of oil products is controlled through operational adjustments in the oil processing plant.

Producing oil derivatives with higher quality than specified can generate economic losses such as: using nobler fractions of oil in products with lower added value, greater consumption of inputs and energy losses. Therefore, to meet the specification and obtain efficiency in the production of derivatives, it is necessary to measure and control the quality of the products.

Due to variations in the characteristics of oil, inputs, processing plant equipment and the environment, adjustments in the parameters of the production plant are necessary to keep the quality of derivatives under control.

The quality of products is measured by laboratory tests carried out from production samples. To monitor and control quality during the period between sampling times and laboratory tests, the literature [[1]](https://www.sciencedirect.com/science/article/abs/pii/S0098135421001022) proposes the use of mathematical empirical or phenomenological models that estimate quality from simple variables to be measured in the production process, such as densities, pressures, temperatures and flows. These variables are measured at much higher rates (in the order of minutes) than the rate of sampling and laboratory testing of the products (in the order of hours). It is known that the quality of a product is temporally dependent on process variables, that is, the measured quality of a production sample is correlated with simple variables observed in the past in the production process.

In this work, it is proposed to use deep learning (*Deep Learning*, DL) to estimate the current (current) quality of a derivative based on the history of production process variables and past quality measurements. It is desired to update the quality estimate at a rate compatible with the measurement rates of the simple process variables, that is, at a rate much higher than the laboratory quality measurement rate.

Models were developed using the framework [TensorFlow](https://www.tensorflow.org/) in code [Python](https://www.python.org/). Linear models, dense neural networks (*Dense Neural Networks*, DNN), convolutional neural networks (*Convolutional Neural Networks*, CNN) and LSTM-type recurrent neural networks (*recurrent neural networks*, RNN) were tested (*long short -term memory*)[[2]](https://www.bioinf.jku.at/publications/older/2604.pdf).

The main challenge addressed here is the availability of the *label* at a rate much lower than the other input variables of the model and the update rate of the model itself.

To enable the training, validation and testing of the model, an objective function (*loss function*) and a validation metric calculation function were created that consider the difference in rate between the *label* and other variables of the model. These special functions created compute the validation goal and metric only for the instants when the *label* is available. The other instants (of the missing *labels*) do not influence the result of the objective function or the validation metric, that is, they do not influence the calculation of the adjustment of weights of the network. In this way, it is avoided to approximate the missing values ​​of the *label*, for example by interpolation, which is not suitable due to the long period of missing data (hour order) in relation to the other process variables (minute order).

The results show the feasibility of this approach of special functions for calculating the goal of validation metrics when the *label* is not available at a rate compatible with the other variables.

#### References

[[1]](https://www.sciencedirect.com/science/article/abs/pii/S0098135421001022) Daniela C.M. de Souza, Luís Cabrita, Cláudia F. Galinha, Tiago J. Rato, Marco S. Reis, "A Spectral AutoML approach for industrial soft sensor development: Validation in an oil refinery plant", Computers & Chemical Engineering, Volume 150, 2021.

[[2]](https://www.bioinf.jku.at/publications/older/2604.pdf) Sepp Hochreiter, Jürgen Schmidhuber, "Long Short-Term Memory", Neural Computation 9(8):1735-1780, 1997.

---

Matrícula: 192.671.150

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
