# GRÁFICO DE LINHAS DE REGRESSÃO JS
## Conceito:
Um gráfico de linhas de regressão é uma representação visual que mostra a relação entre duas variáveis através de uma linha de melhor ajuste (também conhecida como linha de regressão). Essa linha é calculada utilizando métodos estatísticos para minimizar a distância entre os pontos de dados reais e a linha.

O objetivo principal é encontrar uma linha que melhor se ajuste aos dados, o que significa que ela minimize a distância entre os pontos de dados e a própria linha. Existem diferentes métodos para calcular essa linha, como o método dos mínimos quadrados.

## Exemplo de Implementação:
Aqui está um exemplo de como criar um gráfico de linhas de regressão com JavaScript e Chart.js:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Gráfico de Linhas de Regressão</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
  <div style="width: 50%; margin: auto;">
    <canvas id="regressionChart" width="400" height="200"></canvas>
  </div>

  <script>
    const ctxRegression = document.getElementById('regressionChart').getContext('2d');

    // Dados de exemplo
    const data = {
      labels: ['January', 'February', 'March', 'April', 'May', 'June'],
      datasets: [{
        label: 'Data',
        data: [65, 59, 80, 81, 56, 55],
        borderColor: 'rgba(75, 192, 192, 1)',
        borderWidth: 1,
        tension: 0 // Define a tensão da linha para 0 para desativar a interpolação suave
      }, {
        label: 'Regression Line',
        data: [], // Aqui serão adicionados os pontos da linha de regressão
        borderColor: 'rgba(255, 99, 132, 1)',
        borderWidth: 1,
        type: 'line',
        fill: false,
        borderDash: [5, 5] // Define um estilo de linha pontilhada para a linha de regressão
      }]
    };

    // Calculando a linha de regressão
    const x = data.labels.map((_, i) => i); // Valores x são os índices dos dados
    const y = data.datasets[0].data; // Valores y são os dados
    const regression = linearRegression(x, y);

    // Adicionando os pontos da linha de regressão aos dados
    for (let i = 0; i < x.length; i++) {
      data.datasets[1].data.push(regression.slope * i + regression.intercept);
    }

    // Criando o gráfico
    const regressionChart = new Chart(ctxRegression, {
      type: 'line',
      data: data
    });

    // Função para calcular a linha de regressão linear
    function linearRegression(x, y) {
      const n = x.length;
      let sumX = 0;
      let sumY = 0;
      let sumXY = 0;
      let sumX2 = 0;
      for (let i = 0; i < n; i++) {
        sumX += x[i];
        sumY += y[i];
        sumXY += x[i] * y[i];
        sumX2 += x[i] ** 2;
      }
      const slope = (n * sumXY - sumX * sumY) / (n * sumX2 - sumX ** 2);
      const intercept = (sumY - slope * sumX) / n;
      return { slope, intercept };
    }
  </script>
</body>
</html>
```

Neste exemplo, estamos criando um gráfico de linhas com dados de exemplo. Em seguida, calculamos a linha de regressão linear utilizando o método dos mínimos quadrados e a adicionamos ao gráfico. A linha de regressão é representada por uma linha contínua pontilhada. Isso fornece uma representação visual da tendência nos dados e permite fazer previsões com base na relação entre as variáveis.