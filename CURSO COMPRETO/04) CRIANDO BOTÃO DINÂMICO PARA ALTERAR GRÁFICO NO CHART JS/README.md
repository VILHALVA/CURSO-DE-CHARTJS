# CRIANDO BOTÃO DINÂMICO PARA ALTERAR GRÁFICO NO CHART JS
## Conceito:
O objetivo de criar um botão dinâmico para alterar o gráfico no Chart.js é permitir que os usuários interajam com o gráfico e atualizem seus dados ou visualizações conforme necessário. Isso pode ser útil para fornecer uma experiência mais interativa aos usuários, permitindo-lhes explorar diferentes conjuntos de dados ou visualizações dentro do mesmo contexto.

Para implementar isso, você precisa de um botão na página da web que, quando clicado, dispara uma função JavaScript. Esta função JavaScript é responsável por atualizar os dados do gráfico e, em seguida, atualizar o próprio gráfico na tela para refletir as alterações.

## Exemplos de Trechos de Código e Explicações:
### 1. Estrutura HTML com Botão e Gráfico:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dynamic Chart</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
  <canvas id="myChart" width="800" height="400"></canvas>
  <button id="changeButton">Change Data</button>
</body>
</html>
```

- Este trecho de código define a estrutura HTML básica com um elemento `<canvas>` para o gráfico e um botão com o ID `changeButton` para alterar os dados do gráfico.

### 2. Script JavaScript para Criar e Atualizar o Gráfico:
```html
<script>
  // Função para criar o gráfico inicial
  function createChart() {
    const ctx = document.getElementById('myChart').getContext('2d');
    const myChart = new Chart(ctx, {
      type: 'bar',
      data: {
        labels: ['A', 'B', 'C'],
        datasets: [{
          label: 'Data 1',
          data: [10, 20, 30],
          backgroundColor: 'rgba(255, 99, 132, 0.2)',
          borderColor: 'rgba(255, 99, 132, 1)',
          borderWidth: 1
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

    // Adiciona um ouvinte de evento ao botão para chamar a função changeData()
    document.getElementById('changeButton').addEventListener('click', () => {
      changeData(myChart);
    });
  }

  // Função para alterar os dados do gráfico quando o botão for clicado
  function changeData(chart) {
    // Novos dados para o gráfico (gerados aleatoriamente para este exemplo)
    const newData = [Math.random() * 50, Math.random() * 50, Math.random() * 50];

    // Atualiza os dados do gráfico
    chart.data.datasets[0].data = newData;

    // Atualiza o gráfico na tela
    chart.update();
  }

  // Chama a função para criar o gráfico inicialmente
  createChart();
</script>
```

- A função `createChart()` é responsável por criar o gráfico inicialmente quando a página é carregada. Ela também adiciona um ouvinte de evento ao botão, que chama a função `changeData()` quando o botão é clicado.
- A função `changeData(chart)` é responsável por alterar os dados do gráfico quando o botão é clicado. Neste exemplo, os novos dados são gerados aleatoriamente usando `Math.random()`.
- Após a atualização dos dados do gráfico, o método `update()` é chamado para atualizar o gráfico na tela com os novos dados.

Com esses trechos de código, você pode criar um botão dinâmico para alterar o gráfico no Chart.js em sua página da web. Você pode personalizar a lógica dentro da função `changeData()` para atender às suas necessidades específicas de atualização de dados do gráfico.