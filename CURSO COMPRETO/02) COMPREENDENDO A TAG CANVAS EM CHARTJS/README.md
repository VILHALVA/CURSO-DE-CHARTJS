# COMPREENDENDO A TAG CANVAS EM CHARTJS
A tag `<canvas>` é uma parte essencial ao usar Chart.js, pois é onde o gráfico será desenhado na página web. Aqui está uma explicação mais detalhada sobre como a tag `<canvas>` funciona em conjunto com Chart.js:

## 1. Elemento `<canvas>`
A tag `<canvas>` é um elemento HTML5 que fornece uma superfície de desenho bidimensional em que você pode desenhar gráficos, animações, gráficos de jogos, entre outros.

## 2. Uso em Chart.js
Ao usar Chart.js, você precisa adicionar um elemento `<canvas>` ao seu documento HTML para cada gráfico que deseja criar. Este elemento serve como o local onde o gráfico será renderizado.

## 3. Atributos
A tag `<canvas>` pode ter os seguintes atributos importantes:

- `id`: Um identificador único para o elemento canvas, que é usado para referenciá-lo em JavaScript.
- `width` e `height`: Determinam a largura e altura do elemento canvas, respectivamente. Eles podem ser definidos em pixels ou com valores percentuais.

## 4. Contexto de Desenho
Para desenhar gráficos com Chart.js, você precisa obter o contexto de desenho do elemento canvas. Isso é feito usando o método `getContext()` em um elemento `<canvas>`. O contexto de desenho retornado é usado para criar e controlar os gráficos.

```javascript
const canvas = document.getElementById('myCanvas');
const ctx = canvas.getContext('2d');
```

## 5. Chart.js
Chart.js é uma biblioteca JavaScript que facilita a criação de gráficos interativos em uma página web. Ele trabalha em conjunto com o elemento `<canvas>` para desenhar os gráficos.

## 6. Renderização de Gráficos
Quando você cria um novo gráfico com Chart.js, especifica o contexto de desenho do elemento canvas onde o gráfico será renderizado. O Chart.js usa esse contexto para desenhar os elementos do gráfico, como barras, linhas, pontos, legendas, etc.

## Exemplo de Uso:
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
    <canvas id="myChart" width="400" height="400"></canvas>
  </div>
  <script>
    const ctx = document.getElementById('myChart').getContext('2d');
    const myChart = new Chart(ctx, {
      type: 'bar',
      data: {
        labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
        datasets: [{
          label: '# of Votes',
          data: [12, 19, 3, 5, 2, 3],
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
  </script>
</body>
</html>
```

Neste exemplo, um elemento `<canvas>` é usado para criar um gráfico de barras com Chart.js. O contexto de desenho é obtido usando `getContext('2d')` e passado para o construtor de Chart.js. O gráfico é então renderizado no elemento canvas com base nos dados e opções fornecidos.