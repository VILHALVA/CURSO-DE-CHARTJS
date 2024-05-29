# TUTORIAL DE GRÁFICO JS PARA INICIANTES
Aqui está um tutorial básico sobre como criar gráficos usando Chart.js, destinado a iniciantes.

## 1. Introdução e Configuração
### O que é Chart.js?
Chart.js é uma biblioteca JavaScript que permite criar gráficos interativos e responsivos em páginas web. É fácil de usar e oferece uma variedade de tipos de gráficos, como gráficos de barras, linhas, torta, radar, entre outros.

## Instalação
### Via CDN
A maneira mais fácil de começar é incluir Chart.js diretamente de uma CDN. Adicione o seguinte script ao seu arquivo HTML:

```html
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
```

### Via npm (Node.js)
Se você estiver usando um ambiente Node.js, pode instalar Chart.js com npm:

```bash
npm install chart.js
```

## 2. Criando o Primeiro Gráfico
Vamos começar criando um gráfico de barras simples.

### Estrutura HTML Básica
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
    // Código do gráfico aqui
  </script>
</body>
</html>
```

### Código do Gráfico
No script, adicione o código para criar um gráfico de barras:

```javascript
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
```

## 3. Tipos de Gráficos
Chart.js suporta vários tipos de gráficos. Vamos ver como criar alguns dos mais comuns.

### Gráfico de Linhas
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

### Gráfico de Pizza
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

## 4. Personalização de Gráficos
Você pode personalizar quase todos os aspectos de um gráfico Chart.js.

### Exemplo: Alterando a Cor de Fundo e a Cor da Borda
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

## 5. Trabalhando com Dados Dinâmicos
Você pode atualizar um gráfico com novos dados dinamicamente.

### Exemplo: Atualizando os Dados do Gráfico
```javascript
function updateChart(chart, newData) {
  chart.data.datasets[0].data = newData;
  chart.update();
}

const data = [10, 20, 30, 40, 50, 60];
updateChart(myChart, data);
```

## 6. Interatividade e Eventos
Chart.js permite adicionar interatividade aos gráficos.

### Exemplo: Adicionando Eventos de Clique
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

## 7. Exemplos Práticos
Vamos concluir com alguns exemplos práticos que combinam várias técnicas aprendidas:

### Dashboard Simples
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

### Conclusão
Com esses fundamentos e exemplos, você está pronto para começar a usar Chart.js em seus projetos. Conforme você ganha mais experiência, pode explorar a documentação oficial para aprender sobre recursos avançados e personalizações.