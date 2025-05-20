# Azure Inteligência Artificial (IA) - Modelo de Machine Learning
Repositório para documentar o processo de criação de um **modelo de previsão** de aluguel de bicicletas utilizando o **Machine Learning** Sudio do **Microsoft Azure**. Esse é um estudo incentivado pelo bootcamp IA-900, patrocinado pela Microsoft e distribuído pela [DIO](https://web.dio.me/track/microsoft-fundamentos-de-ia).
<br>

![image](https://github.com/user-attachments/assets/7dd10b52-8ef1-4377-b0df-55e94fa12f00)



### Links importantes:
- **Documentação oficial da Microsoft:** [microsoftlearning.github.io/mslearn-ai-fundamentals](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html). <br> O qual descreve passo a passo todo o processo que documentarei a seguir.
 
  
- **Azure:** [azure.microsoft.com](https://azure.microsoft.com/pt-br/get-started/azure-portal/). <br>
  Ferramente utilizada para criação e treinamento do modelo.

## Processo de criação do modelo:
1. Primeiro passo foi criar um **Espaço de trabalho** no Microsoft Azure. Todo o processo foi simples e a plataforma foi bem intuitiva, Descrevendo cada parâmetro desde o inicio. 

2. Próximo passo foi começar um novo **trabalho de Machine Learning Automatizado**. Esse processo foi dentro do chamado **Launch Studio**, do Azure. É nessa etapa que é configurado todo o processo de aprendizado de modelo, incluindo a inserção dos dados, carga de trabalho, quantos algoritmos diferentes serão testados, quantas tentativas serão feitas e parâmetros relacionados à validação. O treinamento é feito numa máquina virtual fornecida pelo Azure, e como se trata de um projeto simples de aprendizado, o processo é relativamente rápido (8 - 15min). Quanto mais algoritmos forem testatos e quanto mais rigoroso for o treinamento e validação, mais processamento será gasto, porém, melhor será o resultado.

3. Com o treinamento feito, já é possível ver alguns resultados. O próximo passo, para poder testar o modelo, é fazer o **deploy**. Processo que é simples e rápido mas que pode gerar alguns erros referentes à [falta de registro em alguns provedores de recursos da Microsoft](https://learn.microsoft.com/en-us/azure/azure-resource-manager/troubleshooting/error-register-resource-provider?tabs=azure-cli) (Caso você tenha se deparado com um erro parecido, essa foi a solução que funcionou pra mim: [learn.microsoft.com](https://learn.microsoft.com/en-us/answers/questions/2129910/resource-provider-(n-a)-isnt-registered-with-subsc)). Com o modelo feito, é possível testá-lo o compará-lo, por conta própria, com a base de dados.

## Resultados
A seguir, alguns gráficos referentes ao resultado do treinamento. **Lembrando que o objetivo foi criar uma IA, com carga de trabalho regressiva, para prever o número de alugueis de bicicletas em determinado dia, com base em alguns dados.**
![image](https://github.com/user-attachments/assets/14af88cb-b95e-401b-bf73-c9dad1cfdb3c)
*(O gráfico acima compara os valores reais e valores previstos)*
<br>
<br>

![image](https://github.com/user-attachments/assets/22555889-249a-4edd-bb5c-440a374e77a5)
*(O gráfico acima mostra a diferença entre os valores reais e os valores previstos)*
<br>
<br>

Feito o deploy, é possível observar esses resultados na prática. Os parâmetros usados para prever o nùmero de alugueis de bicicleta em um dia são: <br>
| Day | Month | Year | Season | Holliday | WeekDay | WorkingDay | Weathersit | Temp | Atempt | Hum | Windspeed |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|--:|
<br>

**Usando os parâmetros do primeiro dia fornecido pela base de dados:** <br>
| Day | Month | Year | Season | Holliday | WeekDay | WorkingDay | Weathersit | Temp | Atempt | Hum | Windspeed |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|--:|
| 1 | 1 | 2011 | 1 | 0 | 6 | 0 | 2 | 0.344167 | 0.363625 | 0.805833 | 0.160446 |
<br>

O **RESULTADO REAL** é: **331 aluguéis** <br>
O **RESULTADO PREVISTO** é (aproximadamente): **450 aluguéis**
<br>
<br>
Confirmando o que foi descrito nos gráficos acima, onde há uma diferença entre os valores previstos e os reais quando pegamos um dos primeiros dias que constam na base de dados. Porém, se pegarmos os dados do último dia que consta na base de dados, essa diferença se inverte.
<br>

**Usando os parâmetros do 732° dia fornecido pela base de dados (último):** <br>
| Day | Month | Year | Season | Holliday | WeekDay | WorkingDay | Weathersit | Temp | Atempt | Hum | Windspeed |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|--:|
| 31 | 12 | 2012 | 1 | 0 | 1 | 1 | 2 | 0.215833 | 0.223487 | 0.5775 | 0.154846 |
<br>

O **RESULTADO REAL** é: **439 aluguéis** <br>
O **RESULTADO PREVISTO** é (aproximadamente): **270 aluguéis**
<br>

Os testes são feitos diretamente pelo **Machine Learning Studio** do Azure, por meio da aba **Endpoints** -> **Tests**, liberada após feito o Deploy. É necessário introduzir os dados de entrada por meio do código: <br>
```
{
  "input_data": {
    "columns": [
      "day",
      "mnth",
      "year",
      "season",
      "holiday",
      "weekday",
      "workingday",
      "weathersit",
      "temp",
      "atemp",
      "hum",
      "windspeed"
    ],
    "index": [0],
    "data": [[1,1,2022,2,0,1,1,2,0.3,0.3,0.3,0.3]]
  }
 }
```

### Conclusões finais:
Foi a minha **primeira experiência com Machine Learning** e a primeira impressão foi bastante positiva, o processo foi tranquilo e foi importante pra dar uma base prática sobre o tema. Foi importante também para me apresentar sobre a ferramente do Microsoft Azure, que oferece muitas opçôes para fazer com que o processo de treinamento da IA seja ainda mais eficiente e próximo da realidade, a impressão que fica é de que a ferramenta é muito poderosa.
<br>




