# MANUAL
## INSTALAÇÃO:
Você pode adicionar Chart.js ao seu projeto de várias maneiras:

### VIA CDN:
Inclua o seguinte script em seu arquivo HTML para importar Chart.js diretamente de uma CDN:
```html
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
```

Usaremos apenas esse método em nosso curso!

### VIA NPM (NODEJS):
Se você estiver usando um ambiente Node.js, instale Chart.js com npm:
```bash
npm install chart.js
```

## CRIANDO O PRIMEIRO GRÁFICO:
Vamos começar criando um gráfico de barras simples.

Crie um arquivo HTML básico com um elemento `<canvas>` onde o gráfico será desenhado:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Chart.js Example</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
  <div style="width: 50%; margin: auto;">
    <canvas id="myChart"></canvas>
  </div>
  <script>
    const ctx = document.getElementById('myChart').getContext('2d');
    const myChart = new Chart(ctx, {
      type: 'bar',  // Tipo de gráfico
      data: {
        labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],  // Rótulos do eixo x
        datasets: [{
          label: '# of Votes',
          data: [12, 19, 3, 5, 2, 3],  // Dados do gráfico
          backgroundColor: [
            'rgba(255, 99, 132, 0.2)',
            'rgba(54, 162, 235, 0.2)',
            'rgba(255, 206, 86, 0.2)',
            'rgba(75, 192, 192, 0.2)',
            'rgba(153, 102, 255, 0.2)',
            'rgba(255, 159, 64, 0.2)'
          ],
          borderColor: [
            'rgba(255, 99, 132, 1)',
            'rgba(54, 162, 235, 1)',
            'rgba(255, 206, 86, 1)',
            'rgba(75, 192, 192, 1)',
            'rgba(153, 102, 255, 1)',
            'rgba(255, 159, 64, 1)'
          ],
          borderWidth: 1  // Largura da borda das barras
        }]
      },
      options: {
        scales: {
          y: {
            beginAtZero: true  // Inicia o eixo y no zero
          }
        }
      }
    });
  </script>
</body>
</html>
```

## TIPOS DE GRÁFICOS:
Chart.js suporta vários tipos de gráficos. Vamos ver como criar alguns dos mais comuns.

### GRÁFICO DE LINHAS:
```javascript
const lineChart = new Chart(ctx, {
  type: 'line',
  data: {
    labels: ['January', 'February', 'March', 'April', 'May', 'June'],
    datasets: [{
      label: 'Sales',
      data: [65, 59, 80, 81, 56, 55],
      fill: false,  // Preenchimento abaixo da linha
      borderColor: 'rgb(75, 192, 192)',
      tension: 0.1  // Suavização das linhas
    }]
  },
  options: {
    scales: {
      y: {
        beginAtZero: true
      }
    }
  }
});
```

### GRÁFICO DE PIZZA:
```javascript
const pieChart = new Chart(ctx, {
  type: 'pie',
  data: {
    labels: ['Red', 'Blue', 'Yellow'],
    datasets: [{
      label: 'Votes',
      data: [12, 19, 3],
      backgroundColor: [
        'rgb(255, 99, 132)',
        'rgb(54, 162, 235)',
        'rgb(255, 205, 86)'
      ],
      hoverOffset: 4
    }]
  }
});
```

## PERSONALIZAÇÃO DE GRÁFICOS:
Você pode personalizar quase todos os aspectos de um gráfico Chart.js.

### EXEMPLO: ALTERANDO A COR DE FUNDO E A COR DA BORDA:
```javascript
const customChart = new Chart(ctx, {
  type: 'bar',
  data: {
    labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
    datasets: [{
      label: '# of Votes',
      data: [12, 19, 3, 5, 2, 3],
      backgroundColor: 'rgba(54, 162, 235, 0.2)',
      borderColor: 'rgba(54, 162, 235, 1)',
      borderWidth: 1
    }]
  },
  options: {
    plugins: {
      legend: {
        display: false  // Esconde a legenda
      }
    },
    scales: {
      y: {
        beginAtZero: true
      }
    }
  }
});
```

## TRABALHANDO COM DADOS DINÂMICOS:
Você pode atualizar um gráfico com novos dados dinamicamente.

### EXEMPLO: ATUALIZANDO OS DADOS DO GRÁFICO:
```javascript
function updateChart(chart, newData) {
  chart.data.datasets[0].data = newData;
  chart.update();
}

const data = [10, 20, 30, 40, 50, 60];
updateChart(myChart, data);
```

## INTERATIVIDADE E EVENTOS:
Chart.js permite adicionar interatividade aos gráficos.

### EXEMPLO: ADICIONANDO EVENTOS DE CLIQUE:
```javascript
myChart.canvas.onclick = function(event) {
  const points = myChart.getElementsAtEventForMode(event, 'nearest', { intersect: true }, false);
  if (points.length) {
    const firstPoint = points[0];
    const label = myChart.data.labels[firstPoint.index];
    const value = myChart.data.datasets[firstPoint.datasetIndex].data[firstPoint.index];
    console.log(`Clicked on: ${label}, value: ${value}`);
  }
};
```

## EXEMPLOS PRÁTICOS:
Vamos concluir com alguns exemplos práticos que combinam várias técnicas aprendidas:

### DASHBOARD SIMPLES:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Chart.js Dashboard</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    .chart-container {
      width: 50%;
      margin: 20px auto;
    }
  </style>
</head>
<body>
  <div class="chart-container">
    <canvas id="salesChart"></canvas>
  </div>
  <div class="chart-container">
    <canvas id="distributionChart"></canvas>
  </div>
  <script>
    const salesCtx = document.getElementById('salesChart').getContext('2d');
    const distributionCtx = document.getElementById('distributionChart').getContext('2d');

    const salesChart = new Chart(salesCtx, {
      type: 'line',
      data: {
        labels: ['January', 'February', 'March', 'April', 'May', 'June'],
        datasets: [{
          label: 'Sales',
          data: [65, 59, 80, 81, 56, 55],
          borderColor: 'rgb(75, 192, 192)',
          tension: 0.1
        }]
      },
      options: {
        scales: {
          y: {
            beginAtZero: true
          }
        }
      }
    });

    const distributionChart = new Chart(distributionCtx, {
      type: 'pie',
      data: {
        labels: ['Red', 'Blue', 'Yellow'],
        datasets: [{
          label: 'Distribution',
          data: [12, 19, 3],
          backgroundColor: [
            'rgb(255, 99, 132)',
            'rgb(54, 162, 235)',
            'rgb(255, 205, 86)'
          ]
        }]
      }
    });
  </script>
</body>
</html>
```

## CONCLUSÃO:
Com esses fundamentos e exemplos, você está pronto para começar a usar Chart.js em seus projetos. Conforme você ganha mais experiência, pode explorar a [documentação oficial](https://www.chartjs.org/docs/latest/) para aprender sobre recursos avançados e personalizações. 