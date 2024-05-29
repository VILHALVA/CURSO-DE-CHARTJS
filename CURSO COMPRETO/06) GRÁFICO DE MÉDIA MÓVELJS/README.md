# GRÁFICO DE MÉDIA MÓVELJS
## Conceito
Uma média móvel é uma forma de suavizar uma série de dados ao criar uma média contínua de um subconjunto dos dados. Em análise de séries temporais, como em dados de mercado de ações, a média móvel ajuda a identificar tendências ao reduzir a variação "ruidosa" nos dados. No exemplo a seguir, usaremos uma média móvel simples de 3 pontos para prever movimentos futuros.

## Implementação da Média Móvel em Chart.js
Vamos criar um gráfico de linha que inclui uma linha de média móvel baseada em um conjunto de dados existente.

### Passos:
1. **Configuração inicial do gráfico de linha**: Criar o gráfico de linha básico usando Chart.js.
2. **Cálculo da média móvel**: Implementar uma função para calcular a média móvel simples.
3. **Adicionar a linha de média móvel ao gráfico**: Incorporar os valores calculados da média móvel como um novo dataset no gráfico.

## Exemplo de Código
### 1. Configuração Inicial do Gráfico de Linha
Crie um arquivo HTML com uma tag `<canvas>` para o gráfico.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Moving Average - Line Chart</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      background-color: #343a40;
      color: white;
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
  <div class="container">
    <canvas id="lineChart" width="800" height="400"></canvas>
  </div>

  <script>
    const ctx = document.getElementById('lineChart').getContext('2d');
    const data = [12, 19, 3, 5, 2, 3, 12, 15, 13, 16, 10, 8];
    const labels = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];

    const lineChartData = {
      labels: labels,
      datasets: [{
        label: 'Original Data',
        data: data,
        borderColor: 'rgba(75, 192, 192, 1)',
        backgroundColor: 'rgba(75, 192, 192, 0.2)',
        fill: false
      }]
    };

    const lineChart = new Chart(ctx, {
      type: 'line',
      data: lineChartData,
      options: {
        plugins: {
          legend: {
            display: true
          }
        }
      }
    });
  </script>
</body>
</html>
```

### 2. Cálculo da Média Móvel
Adicione uma função JavaScript para calcular a média móvel simples com base nos dados existentes.

```html
<script>
  function calculateMovingAverage(data, period) {
    let movingAverage = [];
    for (let i = 0; i < data.length; i++) {
      if (i < period - 1) {
        movingAverage.push(null);  // Não há média móvel para os primeiros pontos
      } else {
        const sum = data.slice(i - period + 1, i + 1).reduce((a, b) => a + b, 0);
        movingAverage.push(sum / period);
      }
    }
    return movingAverage;
  }

  const movingAverageData = calculateMovingAverage(data, 3);
</script>
```

### 3. Adicionar a Linha de Média Móvel ao Gráfico
Atualize o gráfico para incluir a linha de média móvel calculada.

```html
<script>
  lineChartData.datasets.push({
    label: 'Moving Average (3 points)',
    data: movingAverageData,
    borderColor: 'rgba(255, 99, 132, 1)',
    backgroundColor: 'rgba(255, 99, 132, 0.2)',
    fill: false
  });

  lineChart.update();
</script>
```

### Código Completo
Aqui está o código completo do projeto:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Moving Average - Line Chart</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      background-color: #343a40;
      color: white;
      font-family: Arial, sans-serif;
    }
  </style>
</head>
<body>
  <div class="container">
    <canvas id="lineChart" width="800" height="400"></canvas>
  </div>

  <script>
    const ctx = document.getElementById('lineChart').getContext('2d');
    const data = [12, 19, 3, 5, 2, 3, 12, 15, 13, 16, 10, 8];
    const labels = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];

    const lineChartData = {
      labels: labels,
      datasets: [{
        label: 'Original Data',
        data: data,
        borderColor: 'rgba(75, 192, 192, 1)',
        backgroundColor: 'rgba(75, 192, 192, 0.2)',
        fill: false
      }]
    };

    const lineChart = new Chart(ctx, {
      type: 'line',
      data: lineChartData,
      options: {
        plugins: {
          legend: {
            display: true
          }
        }
      }
    });

    function calculateMovingAverage(data, period) {
      let movingAverage = [];
      for (let i = 0; i < data.length; i++) {
        if (i < period - 1) {
          movingAverage.push(null);  // Não há média móvel para os primeiros pontos
        } else {
          const sum = data.slice(i - period + 1, i + 1).reduce((a, b) => a + b, 0);
          movingAverage.push(sum / period);
        }
      }
      return movingAverage;
    }

    const movingAverageData = calculateMovingAverage(data, 3);

    lineChartData.datasets.push({
      label: 'Moving Average (3 points)',
      data: movingAverageData,
      borderColor: 'rgba(255, 99, 132, 1)',
      backgroundColor: 'rgba(255, 99, 132, 0.2)',
      fill: false
    });

    lineChart.update();
  </script>
</body>
</html>
```

### Explicação do Código
1. **Configuração do Gráfico**:
   - Define os dados e rótulos para o gráfico de linha.
   - Cria o gráfico de linha com Chart.js.

2. **Cálculo da Média Móvel**:
   - A função `calculateMovingAverage` calcula a média móvel simples de 3 pontos.
   - Para cada ponto de dados, a função verifica se há suficientes pontos anteriores para calcular a média. Se não, insere `null`.

3. **Atualização do Gráfico**:
   - Adiciona os dados de média móvel ao dataset do gráfico.
   - Atualiza o gráfico para refletir as mudanças.

Essa implementação permite visualizar a linha de média móvel sobre os dados originais, ajudando a identificar tendências de forma mais clara.