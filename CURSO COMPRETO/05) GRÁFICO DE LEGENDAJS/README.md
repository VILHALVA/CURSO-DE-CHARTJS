# GRÁFICO DE LEGENDAJS
## Conceito: 
Chart.js gera automaticamente uma legenda que é incorporada ao canvas, mas às vezes você pode querer personalizar a aparência ou posicionamento da legenda usando HTML e CSS. Para isso, você pode extrair as informações da legenda do gráfico e criar sua própria legenda HTML.

## Passo a Passo:
1. **Configuração do Gráfico**: Crie um gráfico Chart.js com os dados desejados.
2. **Extração da Legenda**: Utilize as opções de legendas personalizadas do Chart.js para obter os dados da legenda.
3. **Criação da Legenda HTML**: Use os dados extraídos para criar elementos HTML que representem a legenda.

### Passo 1: Configuração do Gráfico:
Vamos começar criando um gráfico básico usando Chart.js.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Custom Legend with Chart.js</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    .legend-container {
      display: flex;
      justify-content: center;
      margin-top: 20px;
    }
    .legend-item {
      margin-right: 15px;
      display: flex;
      align-items: center;
    }
    .legend-color {
      width: 20px;
      height: 20px;
      margin-right: 5px;
    }
  </style>
</head>
<body>
  <div class="container">
    <canvas id="myChart" width="800" height="400"></canvas>
    <div id="legend" class="legend-container"></div>
  </div>

  <script>
    const ctx = document.getElementById('myChart').getContext('2d');
    const chartData = {
      labels: ['Red', 'Blue', 'Yellow'],
      datasets: [{
        label: 'Dataset 1',
        data: [10, 20, 30],
        backgroundColor: ['red', 'blue', 'yellow']
      }]
    };

    const myChart = new Chart(ctx, {
      type: 'bar',
      data: chartData,
      options: {
        plugins: {
          legend: {
            display: false, // Disable default legend
            onClick: (e, legendItem) => {
              const index = legendItem.index;
              const ci = myChart;
              const meta = ci.getDatasetMeta(0);
              meta.data[index].hidden = !meta.data[index].hidden;
              ci.update();
            }
          }
        }
      }
    });

    // Função para criar a legenda HTML
    function createCustomLegend(chart) {
      const legendContainer = document.getElementById('legend');
      const { data } = chart;
      const { datasets } = data;

      datasets.forEach((dataset, datasetIndex) => {
        dataset.data.forEach((dataPoint, index) => {
          const legendItem = document.createElement('div');
          legendItem.classList.add('legend-item');

          const colorBox = document.createElement('div');
          colorBox.classList.add('legend-color');
          colorBox.style.backgroundColor = dataset.backgroundColor[index];

          const label = document.createElement('span');
          label.textContent = data.labels[index];

          legendItem.appendChild(colorBox);
          legendItem.appendChild(label);
          legendContainer.appendChild(legendItem);

          // Event listener for clicking on the legend item
          legendItem.addEventListener('click', () => {
            const meta = chart.getDatasetMeta(datasetIndex);
            const item = meta.data[index];
            item.hidden = !item.hidden;
            chart.update();
          });
        });
      });
    }

    // Cria a legenda personalizada ao carregar a página
    createCustomLegend(myChart);
  </script>
</body>
</html>
```

### Explicação:
1. **Estrutura HTML e CSS**:
    - `legend-container`: Div que conterá a legenda personalizada.
    - `legend-item`: Estilo para os itens da legenda.
    - `legend-color`: Estilo para a caixa de cor da legenda.

2. **Configuração do Gráfico**:
    - Cria um gráfico de barras simples com três categorias (`Red`, `Blue`, `Yellow`).
    - Desativa a legenda padrão do Chart.js com `display: false`.

3. **Função `createCustomLegend`**:
    - Extrai os dados do gráfico.
    - Cria elementos HTML para cada item da legenda (`div` com classes `legend-item` e `legend-color`).
    - Adiciona a cor de fundo correspondente para cada item.
    - Adiciona um `span` com o texto da legenda.
    - Adiciona um `eventListener` para cada item, permitindo ocultar/exibir os pontos de dados correspondentes no gráfico ao clicar na legenda.

### Resultados:
Ao carregar a página, você verá:
- O gráfico de barras.
- Uma legenda personalizada abaixo do gráfico, estilizada com HTML e CSS.
- Ao clicar em um item da legenda, a visibilidade dos dados correspondentes no gráfico será alternada.

Este exemplo mostra como criar uma legenda HTML personalizada para um gráfico Chart.js, oferecendo maior flexibilidade para estilização e interação com os dados do gráfico.